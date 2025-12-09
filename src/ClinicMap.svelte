<script>
  import { onMount, onDestroy } from 'svelte';
  import { browser } from '$app/environment';
  import Papa from 'papaparse';
  
  let mapContainer;
  let map;
  let L;
  let markers = [];
  let clinicsData = [];
  let selectedClinic = null;
  let selectedFilters = new Set();
  let searchQuery = '';
  
  // Service categories with colors and icons
  const serviceCategories = {
    abortion: { name: 'Abortion', color: '#FF6B9D', icon: '🏥' },
    birth_control: { name: 'Birth Control', color: '#4ECDC4', icon: '💊' },
    emergency_contraception: { name: 'Emergency Contraception', color: '#95E1D3', icon: '⚡' },
    gender_affirming_care: { name: 'Gender Affirming Care', color: '#F38181', icon: '🏳️‍⚧️' },
    hiv_services: { name: 'HIV Services', color: '#AA96DA', icon: '🔬' },
    mental_health: { name: 'Mental Health', color: '#FCBAD3', icon: '🧠' },
    std_testing_and_treatment: { name: 'STD Testing & Treatment', color: '#FFE66D', icon: '🩺' },
    sexual_and_reproductive_concerns: { name: 'Sexual & Reproductive Concerns', color: '#A8D8EA', icon: '💬' },
    iud_insertion_pain_management: { name: 'IUD Insertion', color: '#FFB6B9', icon: '💉' },
    vaccines: { name: 'Vaccines', color: '#C7CEEA', icon: '💉' },
    wellness_and_preventive_care: { name: 'Wellness & Preventive Care', color: '#B5EAD7', icon: '🌟' },
    pregancy_testing: { name: 'Pregnancy Testing', color: '#E2F0CB', icon: '🧪' },
    prenatal_and_postpartum_services: { name: 'Prenatal & Postpartum', color: '#FFDAC1', icon: '👶' }
  };
  
  // Filter clinics based on selected filters and search
  $: filteredClinics = clinicsData.filter(clinic => {
    // Search filter
    if (searchQuery) {
      const query = searchQuery.toLowerCase();
      const searchableText = `${clinic.clinic} ${clinic.address} ${clinic.county}`.toLowerCase();
      if (!searchableText.includes(query)) return false;
    }
    
    // Service filters
    if (selectedFilters.size > 0) {
      return Array.from(selectedFilters).every(filter => {
        const value = clinic[filter];
        return value && value !== 'null' && value.trim() !== '';
      });
    }
    
    return true;
  });
  
  onMount(async () => {
    if (browser) {
      L = (await import('leaflet')).default;
      await import('leaflet/dist/leaflet.css');
      
      // Load CSV data
      await loadCSVData();
      
      // Initialize map
      initializeMap();
    }
  });
  
  async function loadCSVData() {
    try {
      console.log('🔍 Attempting to load CSV...');
      const response = await fetch('/clinics.csv');
      console.log('📡 Fetch response status:', response.status);
      
      if (!response.ok) {
        console.warn('⚠️ CSV not found, using fallback GeoJSON data');
        // Fallback: Load from your GeoJSON data that's already in the code
        loadFromGeoJSON();
        return;
      }
      
      const csvText = await response.text();
      console.log('📄 CSV text length:', csvText.length);
      
      Papa.parse(csvText, {
        header: true,
        skipEmptyLines: true,
        complete: (results) => {
          console.log('✅ Parse complete!');
          console.log('📊 Total rows parsed:', results.data.length);
          
          clinicsData = results.data.map(row => ({
            ...row,
            latitude: parseFloat(row.latitude),
            longitude: parseFloat(row.longitude)
          })).filter(clinic => 
            !isNaN(clinic.latitude) && !isNaN(clinic.longitude)
          );
          
          console.log('🏥 Valid clinics:', clinicsData.length);
          
          if (map) {
            updateMarkers();
          }
        },
        error: (error) => {
          console.error('❌ Parse error:', error);
          loadFromGeoJSON();
        }
      });
    } catch (error) {
      console.error('❌ Error loading CSV:', error);
      loadFromGeoJSON();
    }
  }
  
  function loadFromGeoJSON() {
    console.log('📍 Loading from GeoJSON fallback');
    // Paste your GeoJSON data here temporarily
    const geojsonData = {
    "type": "FeatureCollection",
    "features": [
        {
            "type": "Feature",
            "properties": {
                "index": "1",
                "clinic": "Redwood City Health Center",
                "address": "2907 El Camino Real Redwood City, CA 94061",
                "county": "San Mateo",
                "website": "https://www.plannedparenthood.org/health-center/california/redwood-city/94061/redwood-city-health-center-4129-90130",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks",
                "birth_control": "in person & telehealth; birth control counseling, emergency contraception pills, fertility awareness methods (FAMs); birth control implant, IUD; birth control patch, birth control ring (NuvaRing), birth control shot; birth control sponge, condoms, spermicide and gel (phexxi);; birth control pill\nimplant (Nexplanon)\nIUD\nnon-hormonal/copper IUD\nhormonal IUD\nbirth control shot (Depo-Provera)",
                "emergency_contraception": "in person & telehealth; IUD as emergency contraception;; Over-the-counter EC pill",
                "gender_affirming_care": "in person & telehealth; surgery referrals, gender affirming hormone therapy",
                "hiv_services": "in person & telehealth; hiv testing, hiv treatment support and referrals",
                "mental_health": "telehealth",
                "std_testing_and_treatment": "in person & telehealth; Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHPV vaccine;; syphilis\ngonorrhea\nchlamydia\nHIV",
                "sexual_and_reproductive_concerns": "in person; Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nInfertility support and referral\nSexual issues\nPremature ejaculation",
                "iud_insertion_pain_management": "non-hormonal/copper IUD\nhormonal IUD",
                "vaccines": "in person; HPV vaccine",
                "wellness_and_preventive_care": "in person & telehealth; Cancer Prevention And Screening\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nColon cancer screening\nTesticular and prostate cancer screening\nWellness Visits And Support\nMenopause treatment\nPostpartum visit\nOther Services\nBehavioral Health Counseling\nMental Health Services\nIntegrated Behavioral Health",
                "languages_offered_in": "Spanish and Cantonese; interpreters available with advance notice",
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.2112366,
                    37.4693498
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "2",
                "clinic": "Concord Health Center",
                "address": "2185 Pacheco Street\nConcord, CA 94520",
                "county": "Contra Costa",
                "website": "https://www.plannedparenthood.org/health-center/california/concord/94520/concord-health-center-3269-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks",
                "birth_control": "BC Implant\nVasectomy \nIUD\nring\nshot\nNuvaRing",
                "emergency_contraception": "Emergency contraception (EC)\nIUD as emergency contraception",
                "gender_affirming_care": null,
                "hiv_services": null,
                "mental_health": null,
                "std_testing_and_treatment": null,
                "sexual_and_reproductive_concerns": null,
                "iud_insertion_pain_management": null,
                "vaccines": null,
                "wellness_and_preventive_care": null,
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.0347415,
                    37.979058
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "3",
                "clinic": "Walnut Creek Health Center",
                "address": "1357 Oakland Blvd.\nWalnut Creek, CA 94596",
                "county": "Contra Costa",
                "website": "https://www.plannedparenthood.org/health-center/california/walnut-creek/94596/walnut-creek-health-center-2571-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks\nIn-Clinic Abortion up to 18 weeks ",
                "birth_control": "Implant \nIUD\nPatch\nPill\nNuvaRing\nShot",
                "emergency_contraception": "EC\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone Therapy\nSurgery Referals \nEducation \nResources ",
                "hiv_services": "HIV Testing\nHIV Treatment support and referrals ",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)",
                "sexual_and_reproductive_concerns": "Infections and irritations\n\nJock itch\nSexual health concerns\nReproductive health concerns\n\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\n\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nWellness Visits And Support\n\nMenopause treatment",
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.0705378,
                    37.8978575
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "4",
                "clinic": "Oakland Health Center",
                "address": "1400 Broadway\nOakland, CA 94612",
                "county": "Alameda",
                "website": "https://www.plannedparenthood.org/health-center/california/oakland/94612/oakland-health-center-21934-90130",
                "database": "Planned Parenthood database",
                "abortion": "Abortion pill up to 11 weeks, in-clinic abortions up to 20 weeks",
                "birth_control": null,
                "emergency_contraception": "Emergency contraception pill (morning after pill)",
                "gender_affirming_care": "Care offered (nonspecific)",
                "hiv_services": "HIV testing and treatment offered",
                "mental_health": "No description",
                "std_testing_and_treatment": "Chlamydia, Gonorrhea, Trich, Herpes, Genital warts, Molluscum, Syphilis\n ",
                "sexual_and_reproductive_concerns": "birth control, pregnancy testing and planning services, prenatal and postpartum services for mothers",
                "iud_insertion_pain_management": "IUD insertion offered, pain management offerings not specified",
                "vaccines": null,
                "wellness_and_preventive_care": null,
                "languages_offered_in": "no information",
                "notes": "accepts Medicaid\nMedicaid Family Planning Benefits Program\nMedicaid for Pregnant Women\nMedi-Cal\nFamily PACT",
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.2709468,
                    37.8043923
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "5",
                "clinic": "El Cerritto Health Center",
                "address": "280 El Cerrito Plaza\nEl Cerrito, CA 94530",
                "county": "Alameda",
                "website": "https://www.plannedparenthood.org/health-center/california/el-cerrito/94530/el-cerrito-health-center-3940-90200",
                "database": "Planned Parenthood database",
                "abortion": "Abortion pill up to 11 weeks, in-clinic abortions up to 13 weeks and 6 days",
                "birth_control": "EC pills, IUD, birth control patch + pill, ring, shot, condoms, cervical cap, spermicide, birth control counseling, fertility awareness methods, birth control implant, IUD, Gel (Phexxi)",
                "emergency_contraception": "Offers emergency contraception pills and IUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy, Surgery referrals, educational resources",
                "hiv_services": "HIV testing and treatment referrals",
                "mental_health": "wellness visits for menopause offered, support for infertility",
                "std_testing_and_treatment": "hepatitis and hpv vaccines, Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) testing",
                "sexual_and_reproductive_concerns": "Checkups for reproductive/sexual health concerns, fibroids, infertility support and referral, resources for sexual health concerns",
                "iud_insertion_pain_management": "IUD insertion offered.",
                "vaccines": "hepatitis B and HPV",
                "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP), Chest/breast cancer screening and referral, Cervical cancer screening (HPV/Pap test), menopause treatment",
                "languages_offered_in": "no available information",
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.2983939,
                    37.8992575
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "6",
                "clinic": "Napa Health Center",
                "address": "935 Trancas Street Unit 4D\nNapa, CA 94558",
                "county": "Napa",
                "website": "https://www.plannedparenthood.org/health-center/california/napa/94558/napa-health-center-2702-90200",
                "database": "Planned Parenthood",
                "abortion": "Abortion pill up to 11 weeks",
                "birth_control": "EC pills, Birth Control Implant, IUD, birth control patch, birth control pill, NuvaRing, birth control shot, birth control sponge, cervical caps, condoms, diaphragm, spermicide and gel(phexxi)",
                "emergency_contraception": "emergency contraception pills, IUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "testing and treatment for Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) / Condoms\nHepatitis B vaccine (first dose)\nHPV vaccine for prevention",
                "sexual_and_reproductive_concerns": "Jock itch\nSexual health concerns, Checkups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": "IUD offered",
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test), menopause treatment",
                "languages_offered_in": "English, Spanish",
                "notes": "Insurance accepted: Anthem Blue Cross\nBlue Shield of California\nContra Costa Health Plan\nOscar Health Plan of California\nPartnership Health Plan of CA",
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.294775,
                    38.3228422
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "7",
                "clinic": "Planned Parenthood- Vallejo Health Center",
                "address": "303 Sacramento St, Vallejo CA 94590",
                "county": "Solano",
                "website": "https://www.plannedparenthood.org/health-center/california/vallejo/94590/centro-de-salud-vallejo-2699-90200?utm_campaign=vallejo-health-center&utm_medium=organic&utm_source=local-listing",
                "database": "Planned Parenthood database",
                "abortion": "depending on the stage of pregnancy they provide an abortion pill up to 11 weeks and 0 days after 1st menstrual period\nAbortion pill is by appointment only\n",
                "birth_control": "birth control implant (Nexplanon)\nIUD\nEmergency contraception pill\nBirth control pill\nBirth control patch\nBirth control shot \nBirth control ring (Nuva Ring)",
                "emergency_contraception": "Emergency contraception pill (morning after pill)",
                "gender_affirming_care": "Hormone therapy",
                "hiv_services": "counseling and confidential (private testing) for HIV",
                "mental_health": "not offered",
                "std_testing_and_treatment": "testing and treatment for Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) / Condoms\nHepatitis B vaccine (first dose)\nHPV vaccine for prevention",
                "sexual_and_reproductive_concerns": "checkups for reproductive/ sexua health concerns are offered via inperson appointment",
                "iud_insertion_pain_management": "IUD insertion offered",
                "vaccines": "HPV Vaccine",
                "wellness_and_preventive_care": "Cervical cancer screening (HPV/Pap test)",
                "languages_offered_in": "English, Spanish",
                "notes": "Insurance accepted: Anthem Blue Cross\nBlue Shield of California\nContra Costa Health Plan\nOscar Health Plan of California\nPartnership Health Plan of CA",
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.259051,
                    38.0997068
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "8",
                "clinic": "Fairfield Health Center",
                "address": "1325 Travis Blvd. #C\nFairfield, CA 94533",
                "county": "Solano",
                "website": "https://www.plannedparenthood.org/health-center/california/fairfield/94533/fairfield-health-center-2700-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks, in-clinic abortion up to 18 weeks",
                "birth_control": "Birth Control implant\nIUD, Birth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot, Birth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Surgery referrals, education, resources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": "available",
                "std_testing_and_treatment": "testing and treatment for Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) / Condoms\nHepatitis B vaccine (first dose)\nHPV vaccine for prevention",
                "sexual_and_reproductive_concerns": "Jock itch\nSexual health concerns, Checkups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": "IUD offered",
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test), menopause treatment",
                "languages_offered_in": "English, Spanish",
                "notes": "Insurance accepted: Anthem Blue Cross\nBlue Shield of California\nContra Costa Health Plan\nOscar Health Plan of California\nPartnership Health Plan of CA",
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.0519842,
                    38.2576276
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "9",
                "clinic": "San Francisco Health Center",
                "address": "1522 Bush Street\nSan Francisco, CA 94109",
                "county": "San Francisco",
                "website": "https://www.plannedparenthood.org/health-center/california/san-francisco/94109/san-francisco-health-center-3997-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks, in-clininc abortion up to 18 weeks",
                "birth_control": "Birth Control implant\nIUD, Birth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot, Birth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraceptions,IUD as concraception",
                "gender_affirming_care": "Hormone therapy, Surgery referrals, educational resources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\n\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Jock itch\nSexual health concerns\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": "IUD",
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": null,
                "languages_offered_in": "English, Spanish",
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.422614,
                    37.7886494
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "10",
                "clinic": "Antioch Health Center",
                "address": "3670 Delta Fair Boulevard\nAntioch, CA 94509",
                "county": "Contra Costa",
                "website": "https://www.plannedparenthood.org/health-center/california/antioch/94509/antioch-health-center-2573-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks; in-clinic abortion up to 13 weeks and 6 days",
                "birth_control": "Education and lifestyle\nBirth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nLow maintenance\nBirth Control implant\nIUD\nUsed on a schedule\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nUsed every time\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": "IUD",
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nWellness Visits And Support\nMenopause treatment\nPostpartum visit",
                "languages_offered_in": "Spanish",
                "notes": "Insurance accepted We accept:\n\nAnthem Blue Cross\nBlue Shield of California\nContra Costa Health Plan\nOscar Health Plan of California\nPartnership Health Plan of CA",
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.8441851,
                    38.0049497
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "11",
                "clinic": "San Rafael Health",
                "address": "2 H Street, San Rafael, Ca94901",
                "county": "Marin",
                "website": "https://www.plannedparenthood.org/health-center/california/antioch/94509/antioch-health-center-2573-90200",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks; in-clinic abortion up to 13 weeks and 6 days",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nVasectomy\nBirth Control implant\nIUD\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": null,
                "vaccines": "\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nWellness Visits And Support\nMenopause treatment\nVasectomy",
                "languages_offered_in": "Spanish",
                "notes": "Pregnancy tetsing section is mising from some pp centers",
                "pregancy_testing": "Adoption information and referrals\nDiscuss all pregnancy options\nPregnancy Dating (Ultrasound)\nPregnancy test\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": "Major Credit/Debit Cards. Cash",
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.5384097,
                    37.9743646
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "13",
                "clinic": "Hayward Health Center",
                "address": "1032 A Street Hayward, CA 94541",
                "county": "Alameda",
                "website": "https://www.plannedparenthood.org/health-center/california/hayward/94541/hayward-health-center-4150-90130",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "\nHormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nInfertility support and referral\nSexual issues\nPremature ejaculation",
                "iud_insertion_pain_management": null,
                "vaccines": "HPV vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nTesticular and prostate cancer screening\nWellness Visits And Support\nMenopause treatment\nPostpartum visit",
                "languages_offered_in": "spanish,",
                "notes": null,
                "pregancy_testing": "Pregnancy Testing And Options\nAdoption information and referrals\nDiscuss all pregnancy options\nPregnancy test\nPregnancy Planning\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.0834222,
                    37.6746302
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "14",
                "clinic": "Mountain View Health Center",
                "address": "2500 California Street\nMountain View, CA 94040",
                "county": "Santa Clara",
                "website": "https://www.plannedparenthood.org/health-center/california/mountain-view/94040/mountain-view-health-center-2310-90130",
                "database": "Planned Parenthood",
                "abortion": "abortion pill up to 11 weeks",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "STD/STI Services\nTesting and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nInfertility support and referral\nSexual issues\nPremature ejaculation",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine\nFlu vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nColon cancer screening\nTesticular and prostate cancer screening\nPrimary Care Screening\nAnemia testing\nCholesterol screening\nDiabetes screening\nHigh blood pressure screening\nThyroid screening\nWellness Visits And Support\nMenopause treatment\nPostpartum visit($55 - $128)\nSmoking cessation\nWellness visit (annual exam, routine check up, etc.)",
                "languages_offered_in": "Spanish, tagalog, hindi",
                "notes": null,
                "pregancy_testing": "Pregnancy Testing And Options\nAdoption information and referrals\nDiscuss all pregnancy options\nPregnancy test($15 - $25)\nPregnancy Planning\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": null,
                "prenatal_and_postpartum_services": "Miscarriage And Postpartum Care\nMiscarriage care and support\nPostpartum visit($55 - $128)\nOther Services\nDiscuss all pregnancy options\nPregnancy test($15 - $25)"
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.1061518,
                    37.4034925
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "15",
                "clinic": "Hilltop-Richmond Health Center",
                "address": "2970 Hilltop Mall Road #307\nRichmond, CA 94806",
                "county": "Contra Costa",
                "website": "https://www.plannedparenthood.org/health-center/california/richmond/94806/hilltop-richmond-health-center-2791-90200",
                "database": "Planned Parenthood",
                "abortion": "Abortion: up to 11 weeks\nIn-clinic: up to 13 weeks and 6 days",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": "offered?",
                "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
                "iud_insertion_pain_management": null,
                "vaccines": "Vaccine services\nHepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nWellness Visits And Support\nMenopause treatment",
                "languages_offered_in": "spanish",
                "notes": null,
                "pregancy_testing": "Pregnancy Testing And Options\nAdoption information and referrals\nDiscuss all pregnancy options\nPregnancy Dating (Ultrasound)\nPregnancy test\nPregnancy Planning\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.3292435,
                    37.9775811
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "16",
                "clinic": "San Jose Central Health Center",
                "address": "1691 The Alameda\nSan Jose, CA 95126",
                "county": "Santa Clara",
                "website": "https://www.plannedparenthood.org/health-cent",
                "database": "Planned Parenthood",
                "abortion": "Abortion: up to 11 weeks\nIn-clinic: up to 13 weeks and 6 days",
                "birth_control": "Birth control counseling\nEmergency contraception pills($20 - $40)\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills($20 - $40)\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nInfertility support and referral\nSexual issues\nPremature ejaculation",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine\nFlu vaccine",
                "wellness_and_preventive_care": "Cancer Prevention And Screening\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nColon cancer screening\nTesticular and prostate cancer screening\nPrimary Care Screening\nAnemia testing\nCholesterol screening\nDiabetes screening\nHigh blood pressure screening\nThyroid screening\nWellness Visits And Support\nMenopause treatment\nPostpartum visit\nMedi-cal only\nSmoking cessation\nWellness visit (annual exam, routine check up, etc.)\nOther Services\nTuberculosis testing\nTreatment of acute illness\nManagement of chronic diseases",
                "languages_offered_in": "Spanish, Vietnamese, Tagalog, Hindi, Urdu and Mandarin",
                "notes": null,
                "pregancy_testing": "Pregnancy Testing And Options\nAdoption information and referrals\nDiscuss all pregnancy options\nPregnancy test($15 - $25)\nPregnancy Planning\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": null,
                "prenatal_and_postpartum_services": "Prenatal Planning\nPrenatal services and referrals\n(Medi-cal only)\nMiscarriage And Postpartum Care\nMiscarriage care and support\nPostpartum visit\nMedi-cal only\nOther Services\nDiscuss all pregnancy options\nPregnancy test($15 - $25)"
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.9196217,
                    37.3371379
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "17",
                "clinic": "Blossom Hill Health Center",
                "address": "5440 Thornwood Drive\nSan Jose, CA 95123",
                "county": "Santa Clara",
                "website": "https://www.plannedparenthood.org/health-center/california/san-jose/95123/blossom-hill-health-center-3230-90130",
                "database": "Planned Parenthood",
                "abortion": "Abortion Pill: Up to 11 weeks",
                "birth_control": "Birth control counseling\nEmergency contraception pills\n($40)\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\n($40)\nIUD as emergency contraception",
                "gender_affirming_care": "Surgery referrals\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nInfertility support and referral\nSexual issues\nPremature ejaculation",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine (first dose)\nHPV vaccine\nFlu vaccine",
                "wellness_and_preventive_care": "Chest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\nColon cancer screening\nTesticular and prostate cancer screening\nAnemia testing\nCholesterol screening\nDiabetes screening",
                "languages_offered_in": "Spanish, Mandarin and Tagalog",
                "notes": null,
                "pregancy_testing": "Adoption information and referrals\nDiscuss all pregnancy options\nPregnancy test($20 - $60)\nFertility and pregnancy planning\nInfertility support and referral",
                "payment_information": null,
                "prenatal_and_postpartum_services": "Miscarriage care and support\nPostpartum visit\nDiscuss all pregnancy options\nPregnancy test($20 - $60)"
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.8606196,
                    37.2537859
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "18",
                "clinic": "Eastside Health Center",
                "address": "3131 Alum Rock Avenue\nSan Jose, CA 95127",
                "county": "Santa Clara",
                "website": "https://www.plannedparenthood.org/health-center/california/san-jose/95127/eastside-health-center-2435-90130",
                "database": "Planned Parenthood",
                "abortion": null,
                "birth_control": null,
                "emergency_contraception": null,
                "gender_affirming_care": null,
                "hiv_services": null,
                "mental_health": null,
                "std_testing_and_treatment": null,
                "sexual_and_reproductive_concerns": null,
                "iud_insertion_pain_management": null,
                "vaccines": null,
                "wellness_and_preventive_care": null,
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.8275701,
                    37.3666223
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "19",
                "clinic": "Mar Monte Community Clinic",
                "address": "\n1694 Tully Road Suite 40\nSan Jose, CA 95122",
                "county": "Santa Clara",
                "website": "https://www.plannedparenthood.org/health-center/california/san-jose/95122/mar-monte-community-clinic-2437-90130",
                "database": "Planned Parenthood",
                "abortion": null,
                "birth_control": null,
                "emergency_contraception": null,
                "gender_affirming_care": null,
                "hiv_services": null,
                "mental_health": null,
                "std_testing_and_treatment": null,
                "sexual_and_reproductive_concerns": null,
                "iud_insertion_pain_management": null,
                "vaccines": null,
                "wellness_and_preventive_care": null,
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.8257924,
                    37.3211119
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "20",
                "clinic": "San Ramon Health Center",
                "address": "200 Porter Drive, Suite 200, San Ramon, CA 94583",
                "county": "Contra Costa",
                "website": "https://www.plannedparenthood.org/health-center/california/san-ramon/94583/centro-de-salud-san-ramon-2572-90200",
                "database": "Planned Parenthood",
                "abortion": "Abortion pill up to 11 week",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)Birth Control implant\nIUD Birth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot Birth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) Condoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Jock itch\nSexual health concerns Checkups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral\n",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test) Menopause treatment\n\n",
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": "Cash",
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -121.9903758,
                    37.7737615
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "21",
                "clinic": "Santa Rosa Health Center",
                "address": "1140 Sonoma Avenue Building 3, Santa Rosa, CA 95405",
                "county": "Sonoma",
                "website": "https://www.plannedparenthood.org/health-center/california/santa-rosa/95405/santa-rosa-health-center-3990-90200",
                "database": "Planned Parenthood",
                "abortion": "Abortion pill up to 11 week, in-clinic abortion up to 13 weeks and 6 days",
                "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\n\nBirth Control implant\nIUD\n\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nUsed every time\n\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
                "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
                "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
                "hiv_services": "HIV testing\nHIV treatment support and referrals",
                "mental_health": null,
                "std_testing_and_treatment": "Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\n\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "sexual_and_reproductive_concerns": "Jock itch\nSexual health concerns\n\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral\n",
                "iud_insertion_pain_management": null,
                "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine",
                "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\nChest/breast cancer screening and referral\nCervical cancer screening (HPV/Pap test)\n\nMenopause treatment",
                "languages_offered_in": null,
                "notes": null,
                "pregancy_testing": null,
                "payment_information": "Cash",
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.6994749,
                    38.4403225
                ]
            }
        },
        {
            "type": "Feature",
            "properties": {
                "index": "22",
                "clinic": "Vallejo Health Center",
                "address": "303 Sacramento Street\nVallejo, CA 94590",
                "county": "Sonoma",
                "website": "https://www.plannedparenthood.org/health-center/california/vallejo/94590/vallejo-health-center-2699-90200",
                "database": "Planned Parenthood",
                "abortion": "Abortion Pill\nUp to 11 weeks",
                "birth_control": null,
                "emergency_contraception": null,
                "gender_affirming_care": null,
                "hiv_services": null,
                "mental_health": null,
                "std_testing_and_treatment": null,
                "sexual_and_reproductive_concerns": null,
                "iud_insertion_pain_management": null,
                "vaccines": null,
                "wellness_and_preventive_care": null,
                "languages_offered_in": "English, Spanish",
                "notes": null,
                "pregancy_testing": null,
                "payment_information": null,
                "prenatal_and_postpartum_services": null
            },
            "geometry": {
                "type": "Point",
                "coordinates": [
                    -122.259051,
                    38.0997068
                ]
            }
        }
    ]
};
    
    clinicsData = geojsonData.features.map(feature => ({
      index: feature.id,
      clinic: feature.properties.clinic,
      address: feature.properties.address,
      county: feature.properties.county,
      website: feature.properties.website,
      abortion: feature.properties.abortion,
      birth_control: feature.properties.birth_control,
      emergency_contraception: feature.properties.emergency_contraception,
      gender_affirming_care: feature.properties.gender_affirming_care,
      hiv_services: feature.properties.hiv_services,
      mental_health: feature.properties.mental_health,
      std_testing_and_treatment: feature.properties.std_testing_and_treatment,
      sexual_and_reproductive_concerns: feature.properties.sexual_and_reproductive_concerns,
      iud_insertion_pain_management: feature.properties.iud_insertion_pain_management,
      vaccines: feature.properties.vaccines,
      wellness_and_preventive_care: feature.properties.wellness_and_preventive_care,
      languages_offered_in: feature.properties.languages_offered_in,
      notes: feature.properties.notes,
      pregancy_testing: feature.properties.pregancy_testing,
      payment_information: feature.properties.payment_information,
      prenatal_and_postpartum_services: feature.properties.prenatal_and_postpartum_services,
      latitude: feature.geometry.coordinates[1],
      longitude: feature.geometry.coordinates[0]
    }));
    
    console.log('🏥 Loaded from GeoJSON:', clinicsData.length);
    
    if (map) {
      updateMarkers();
    }
  }
  
  function initializeMap() {
    map = L.map(mapContainer).setView([37.8716, -122.2727], 10);
    
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors',
      maxZoom: 19
    }).addTo(map);
    
    if (clinicsData.length > 0) {
      updateMarkers();
    }
  }
  
  function updateMarkers() {
    console.log('🔄 updateMarkers called');
    console.log('🏥 Filtered clinics count:', filteredClinics.length);
    console.log('🗺️ Map object:', map);
    
    // Clear existing markers
    markers.forEach(marker => map.removeLayer(marker));
    markers = [];
    
    console.log('🧹 Cleared old markers');
    
    // Add markers for filtered clinics
    filteredClinics.forEach((clinic, index) => {
      console.log(`📍 Adding marker ${index + 1}:`, clinic.clinic, clinic.latitude, clinic.longitude);
      
      const markerColor = getMarkerColor(clinic);
      
      const customIcon = L.divIcon({
        className: 'custom-marker',
        html: `<div class="marker-pin" style="background-color: ${markerColor};"></div>`,
        iconSize: [30, 42],
        iconAnchor: [15, 42],
        popupAnchor: [0, -42]
      });
      
      const marker = L.marker([clinic.latitude, clinic.longitude], { icon: customIcon })
        .addTo(map)
        .on('click', () => {
          console.log('🖱️ Marker clicked:', clinic.clinic);
          selectedClinic = clinic;
        });
      
      markers.push(marker);
    });
    
    console.log('✅ Total markers added:', markers.length);
    
    // Fit bounds if there are markers
    if (markers.length > 0) {
      const group = L.featureGroup(markers);
      const bounds = group.getBounds();
      console.log('🎯 Fitting bounds:', bounds);
      map.fitBounds(bounds.pad(0.1));
    } else {
      console.warn('⚠️ No markers to display!');
    }
  }
  
  function getMarkerColor(clinic) {
    if (selectedFilters.size === 0) return '#7B3FF2';
    
    // Return color of first active service
    for (const filter of selectedFilters) {
      const value = clinic[filter];
      if (value && value !== 'null' && value.trim() !== '') {
        return serviceCategories[filter]?.color || '#7B3FF2';
      }
    }
    return '#7B3FF2';
  }
  
  function toggleFilter(category) {
    if (selectedFilters.has(category)) {
      selectedFilters.delete(category);
    } else {
      selectedFilters.add(category);
    }
    selectedFilters = selectedFilters;
    updateMarkers();
  }
  
  function clearFilters() {
    selectedFilters.clear();
    selectedFilters = selectedFilters;
    searchQuery = '';
    updateMarkers();
  }
  
  function hasService(clinic, service) {
    const value = clinic[service];
    return value && value !== 'null' && value.trim() !== '';
  }
  
  function getServiceDetails(clinic, service) {
    const value = clinic[service];
    if (!value || value === 'null' || value.trim() === '') {
      return { text: 'Not Available', available: false };
    }
    return { text: value, available: true };
  }
  
  $: if (map && clinicsData.length > 0) {
    updateMarkers();
  }
  
  onDestroy(() => {
    if (map) map.remove();
  });
</script>

<div class="map-layout">
  <!-- Filters Panel -->
  <div class="filters-panel">
    <div class="filters-header">
      <h3>Filter Services</h3>
      <button class="clear-btn" on:click={clearFilters}>Clear All</button>
    </div>
    
    <div class="search-box">
      <input 
        type="text" 
        placeholder="Search clinics..."
        bind:value={searchQuery}
      />
    </div>
    
    <div class="filter-chips">
      {#each Object.entries(serviceCategories) as [key, category]}
        <button 
          class="filter-chip"
          class:active={selectedFilters.has(key)}
          style="--chip-color: {category.color}"
          on:click={() => toggleFilter(key)}
        >
          <span class="chip-icon">{category.icon}</span>
          <span class="chip-text">{category.name}</span>
          {#if selectedFilters.has(key)}
            <span class="chip-check">✓</span>
          {/if}
        </button>
      {/each}
    </div>
    
    <div class="results-count">
      Showing {filteredClinics.length} of {clinicsData.length} clinics
    </div>
  </div>

  <!-- Map -->
  <div class="map-wrapper">
    <div bind:this={mapContainer} class="map-container"></div>
  </div>

  <!-- Clinic Details Sidebar -->
  {#if selectedClinic}
    <div class="details-sidebar">
      <div class="sidebar-header">
        <h2>{selectedClinic.clinic}</h2>
        <button class="close-btn" on:click={() => selectedClinic = null}>×</button>
      </div>
      
      <div class="sidebar-content">
        <div class="info-section">
          <h4>📍 Location</h4>
          <p>{selectedClinic.address}</p>
          <p><strong>County:</strong> {selectedClinic.county}</p>
        </div>

        {#if selectedClinic.website && selectedClinic.website !== 'null'}
          <div class="info-section">
            <h4>🌐 Website</h4>
            <a href={selectedClinic.website} target="_blank" rel="noopener">
              Visit Website →
            </a>
          </div>
        {/if}

        {#if selectedClinic.payment_information && selectedClinic.payment_information !== 'null'}
          <div class="info-section">
            <h4>💳 Payment Information</h4>
            <p>{selectedClinic.payment_information}</p>
          </div>
        {/if}

        {#if selectedClinic.languages_offered_in && selectedClinic.languages_offered_in !== 'null'}
          <div class="info-section">
            <h4>🗣️ Languages Offered</h4>
            <p>{selectedClinic.languages_offered_in}</p>
          </div>
        {/if}

        {#if selectedClinic.notes && selectedClinic.notes !== 'null'}
          <div class="info-section">
            <h4>📝 Notes</h4>
            <p>{selectedClinic.notes}</p>
          </div>
        {/if}

        <div class="services-section">
          <h4>🏥 Services & Details</h4>
          
          {#each Object.entries(serviceCategories) as [key, category]}
            {@const service = getServiceDetails(selectedClinic, key)}
            <div class="service-item" class:unavailable={!service.available}>
              <div class="service-header">
                <span class="service-icon">{category.icon}</span>
                <span class="service-name">{category.name}</span>
                <span class="service-status" class:available={service.available}>
                  {service.available ? '✓' : '✗'}
                </span>
              </div>
              {#if service.available}
                <div class="service-details">
                  {service.text}
                </div>
              {/if}
            </div>
          {/each}
        </div>
      </div>
    </div>
  {/if}
</div>

<style>
  .map-layout {
    display: grid;
    grid-template-columns: 320px 1fr;
    height: 600px;
    background: #1c0333;
    position: relative;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 20px rgba(0,0,0,0.1);
  }

  /* Filters Panel */
  .filters-panel {
    background: white;
    padding: 20px;
    overflow-y: auto;
    border-right: 1px solid #e0e0e0;
  }

  .filters-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 16px;
  }

  .filters-header h3 {
    margin: 0;
    font-size: 1.2rem;
    color: #333;
  }

  .clear-btn {
    background: transparent;
    border: 1px solid #ddd;
    padding: 6px 12px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.8rem;
    color: #666;
    transition: all 0.2s;
  }

  .clear-btn:hover {
    background: #f5f5f5;
    border-color: #7B3FF2;
    color: #7B3FF2;
  }

  .search-box {
    margin-bottom: 16px;
  }

  .search-box input {
    width: 100%;
    padding: 10px;
    border: 2px solid #e0e0e0;
    border-radius: 8px;
    font-size: 0.9rem;
    transition: border-color 0.2s;
  }

  .search-box input:focus {
    outline: none;
    border-color: #7B3FF2;
  }

  .filter-chips {
    display: flex;
    flex-direction: column;
    gap: 8px;
    margin-bottom: 16px;
  }

  .filter-chip {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 10px 12px;
    background: white;
    border: 2px solid #e0e0e0;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s;
    font-size: 0.85rem;
    text-align: left;
  }

  .filter-chip:hover {
    border-color: var(--chip-color);
    transform: translateX(4px);
  }

  .filter-chip.active {
    background: var(--chip-color);
    border-color: var(--chip-color);
    color: white;
    font-weight: 500;
  }

  .chip-icon {
    font-size: 1.1rem;
  }

  .chip-text {
    flex: 1;
  }

  .chip-check {
    font-weight: bold;
  }

  .results-count {
    padding: 10px;
    background: #f0f0f0;
    border-radius: 8px;
    text-align: center;
    font-size: 0.85rem;
    color: #666;
  }

  /* Map */
  .map-wrapper {
    position: relative;
  }

  .map-container {
    height: 100%;
    width: 100%;
  }

  /* Custom marker styling */
  :global(.custom-marker) {
    background: transparent;
    border: none;
  }
  
  :global(.marker-pin) {
    width: 30px;
    height: 30px;
    border-radius: 50% 50% 50% 0;
    position: absolute;
    transform: rotate(-45deg);
    left: 50%;
    top: 50%;
    margin: -15px 0 0 -15px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.3);
    transition: all 0.2s;
  }
  
  :global(.marker-pin::after) {
    content: '';
    width: 14px;
    height: 14px;
    margin: 8px 0 0 8px;
    background: #fff;
    position: absolute;
    border-radius: 50%;
  }

  :global(.custom-marker:hover .marker-pin) {
    transform: rotate(-45deg) scale(1.15);
  }

  /* Details Sidebar */
  .details-sidebar {
    position: absolute;
    right: 0;
    top: 0;
    bottom: 0;
    width: 400px;
    background: white;
    box-shadow: -4px 0 20px rgba(0,0,0,0.15);
    display: flex;
    flex-direction: column;
    z-index: 1000;
  }

  .sidebar-header {
    padding: 20px;
    border-bottom: 1px solid #e0e0e0;
    display: flex;
    justify-content: space-between;
    align-items: start;
    background: linear-gradient(135deg, #7B3FF2 0%, #9D5FF5 100%);
    color: white;
  }

  .sidebar-header h2 {
    margin: 0;
    font-size: 1.3rem;
    flex: 1;
  }

  .close-btn {
    background: rgba(255,255,255,0.2);
    border: none;
    font-size: 2rem;
    color: white;
    cursor: pointer;
    padding: 0;
    width: 36px;
    height: 36px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 6px;
    transition: all 0.2s;
  }

  .close-btn:hover {
    background: rgba(255,255,255,0.3);
  }

  .sidebar-content {
    flex: 1;
    overflow-y: auto;
    padding: 20px;
  }

  .info-section {
    margin-bottom: 20px;
    padding-bottom: 16px;
    border-bottom: 1px solid #f0f0f0;
  }

  .info-section h4 {
    margin: 0 0 10px 0;
    font-size: 0.95rem;
    color: #7B3FF2;
    font-weight: 600;
  }

  .info-section p {
    margin: 4px 0;
    color: #555;
    line-height: 1.5;
    font-size: 0.9rem;
  }

  .info-section a {
    color: #7B3FF2;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.9rem;
  }

  .info-section a:hover {
    text-decoration: underline;
  }

  .services-section {
    margin-top: 20px;
  }

  .services-section h4 {
    margin: 0 0 16px 0;
    font-size: 1rem;
    color: #7B3FF2;
    font-weight: 600;
  }

  .service-item {
    margin-bottom: 12px;
    padding: 12px;
    background: #f9f9f9;
    border-radius: 8px;
    border: 1px solid #e0e0e0;
    transition: all 0.2s;
  }

  .service-item:hover {
    background: #f5f5f5;
  }

  .service-item.unavailable {
    opacity: 0.4;
    background: #fafafa;
  }

  .service-header {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 6px;
  }

  .service-icon {
    font-size: 1.1rem;
  }

  .service-name {
    flex: 1;
    font-weight: 600;
    color: #333;
    font-size: 0.85rem;
  }

  .service-status {
    font-weight: bold;
    color: #ccc;
    font-size: 1.1rem;
  }

  .service-status.available {
    color: #4CAF50;
  }

  .service-details {
    font-size: 0.8rem;
    color: #666;
    line-height: 1.4;
    padding-left: 28px;
    white-space: pre-wrap;
  }

  /* Responsive */
  @media (max-width: 1200px) {
    .map-layout {
      grid-template-columns: 1fr;
      grid-template-rows: auto 1fr;
      height: 800px;
    }

    .filters-panel {
      max-height: 250px;
      border-right: none;
      border-bottom: 1px solid #e0e0e0;
    }

    .details-sidebar {
      width: 100%;
      max-width: 500px;
    }
  }

  @media (max-width: 768px) {
    .details-sidebar {
      width: 100%;
      max-width: none;
    }
  }
</style>