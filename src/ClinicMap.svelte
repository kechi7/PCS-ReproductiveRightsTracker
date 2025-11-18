<script>
  import { onMount } from 'svelte';
  import { browser } from '$app/environment';
  
  let mapContainer;
  let map;
  let L; // Declare L here, import it later
  
  // Your GeoJSON data (replace with your actual data or fetch it)
  let clinicData = {
    "type": "FeatureCollection",
    "features": [
        {
        "type": "Feature",
        "properties": {
            "clinic": "Reproductive Science Center",
            "address": "1100 Park Place Suite 80 San Mateo, California 94403",
            "county": "San Mateo",
            "website": "https://rscbayarea.com/locations/san-mateo-fertility-center/",
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
            "notes": "need to call and ask about treatments offered",
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.2907748,
            37.5451928
            ],
            "type": "Point"
        },
        "id": 0
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Palo Alto Medical Foundation -- Burlingame Center",
            "address": "1501 Trousdale Drive, Building B, Burlingame, CA 94010",
            "county": "San Mateo",
            "website": "https://www.sutterhealth.org/find-location/facility/burlingame-center",
            "abortion": "procedure through 13 weeks, 6 days; pill through 10 weeks, 0 days",
            "birth_control": "birth control pill\nimplant (Nexplanon)\nIUD\nnon-hormonal/copper IUD\nhormonal IUD\nbirth control shot (Depo-Provera)\nsterilization\ntubal ligation (\"getting your tubes tied\")",
            "emergency_contraception": "Prescription EC pill (ella)\r\nOver-the-counter EC pill",
            "gender_affirming_care": null,
            "hiv_services": null,
            "mental_health": null,
            "std_testing_and_treatment": "syphilis\r\nherpes\r\ngonorrhea\r\nchlamydia\r\nHIV",
            "sexual_and_reproductive_concerns": null,
            "iud_insertion_pain_management": "non-hormonal/copper IUD\r\nhormonal IUD",
            "vaccines": null,
            "wellness_and_preventive_care": null,
            "languages_offered_in": "interpretation services; english, hindi, spanish, urdu",
            "notes": "https://www.abortionfinder.org/provider/111709-palo-alto-medical-foundation-burlingame-center",
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.3833296,
            37.5918122
            ],
            "type": "Point"
        },
        "id": 1
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Palo Alto Medical Foundation -- San Carlos Center",
            "address": "301 Industrial Road, San Carlos, CA 94070",
            "county": "San Mateo",
            "website": "https://www.sutterhealth.org/find-location/facility/san-carlos-center",
            "abortion": "abortion procedure through 13 weeks, 6 days; pill through 10 weeks, 0 days",
            "birth_control": "birth control pill\r\nimplant (Nexplanon)\r\nIUD\r\nnon-hormonal/copper IUD\r\nhormonal IUD\r\nbirth control shot (Depo-Provera)\r\nsterilization\r\ntubal ligation (\"getting your tubes tied\")",
            "emergency_contraception": "Prescription EC pill (ella)\r\nOver-the-counter EC pill",
            "gender_affirming_care": null,
            "hiv_services": null,
            "mental_health": null,
            "std_testing_and_treatment": "Sexually Transmitted Infection (STI) Testing\r\nsyphilis\r\nherpes\r\ngonorrhea\r\nchlamydia\r\nHIV",
            "sexual_and_reproductive_concerns": null,
            "iud_insertion_pain_management": "non-hormonal/copper IUD\r\nhormonal IUD",
            "vaccines": null,
            "wellness_and_preventive_care": null,
            "languages_offered_in": "interpretation services; english, cantonese chinese, mandarin chinese, spanish",
            "notes": null,
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.260346,
            37.5154129
            ],
            "type": "Point"
        },
        "id": 2
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Redwood City Health Center",
            "address": "2907 El Camino Real Redwood City, CA 94061",
            "county": "San Mateo",
            "website": "https://www.plannedparenthood.org/health-center/california/redwood-city/94061/redwood-city-health-center-4129-90130",
            "abortion": "abortion pill up to 11 weeks",
            "birth_control": "in person & telehealth; birth control counseling, emergency contraception pills, fertility awareness methods (FAMs); birth control implant, IUD; birth control patch, birth control ring (NuvaRing), birth control shot; birth control sponge, condoms, spermicide and gel (phexxi);; birth control pill\nimplant (Nexplanon)\nIUD\nnon-hormonal/copper IUD\nhormonal IUD\nbirth control shot (Depo-Provera)",
            "emergency_contraception": "in person & telehealth; IUD as emergency contraception;; Over-the-counter EC pill",
            "gender_affirming_care": "in person & telehealth; surgery referrals, gender affirming hormone therapy",
            "hiv_services": "in person & telehealth; hiv testing, hiv treatment support and referrals",
            "mental_health": "telehealth",
            "std_testing_and_treatment": "in person & telehealth; Testing and Treatment\r\nChlamydia\r\nGenital warts\r\nGonorrhea\r\nHerpes\r\nSyphilis\r\nTrichomoniasis (trich)\r\nSTD/STI Prevention\r\nCondoms\r\nHPV vaccine;; syphilis\r\ngonorrhea\r\nchlamydia\r\nHIV",
            "sexual_and_reproductive_concerns": "in person; Infections and irritations\r\nJock itch\r\nSexual health concerns\r\nReproductive health concerns\r\nCheckups for reproductive/sexual health concerns\r\nInfertility support and referral\r\nSexual issues\r\nPremature ejaculation",
            "iud_insertion_pain_management": "non-hormonal/copper IUD\r\nhormonal IUD",
            "vaccines": "in person; HPV vaccine",
            "wellness_and_preventive_care": "in person & telehealth; Cancer Prevention And Screening\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test)\r\nColon cancer screening\r\nTesticular and prostate cancer screening\r\nWellness Visits And Support\r\nMenopause treatment\r\nPostpartum visit\r\nOther Services\r\nBehavioral Health Counseling\r\nMental Health Services\r\nIntegrated Behavioral Health",
            "languages_offered_in": "Spanish and Cantonese; interpreters available with advance notice",
            "notes": null,
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.2112366,
            37.4693498
            ],
            "type": "Point"
        },
        "id": 3
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Palo Alto Medical Foundation -- Redwood City Women's Health",
            "address": "2950 Whipple Avenue, Redwood City, CA 94062",
            "county": "San Mateo",
            "website": "https://www.sutterhealth.org/find-location/facility/redwood-city-women-s-health-center-1043247030",
            "abortion": "abortion services through 14 weeks, 6 days; abortion pill through 10 weeks, 0 days",
            "birth_control": "birth control pill\r\nimplant (Nexplanon)\r\nIUD\r\nnon-hormonal/copper IUD\r\nhormonal IUD\r\nbirth control shot (Depo-Provera)\r\nsterilization\r\ntubal ligation (\"getting your tubes tied\")",
            "emergency_contraception": "Prescription EC pill (ella)\r\nOver-the-counter EC pill",
            "gender_affirming_care": null,
            "hiv_services": null,
            "mental_health": null,
            "std_testing_and_treatment": "syphilis\r\nherpes\r\ngonorrhea\r\nchlamydia\r\nHIV",
            "sexual_and_reproductive_concerns": null,
            "iud_insertion_pain_management": "non-hormonal/copper IUD\r\nhormonal IUD",
            "vaccines": null,
            "wellness_and_preventive_care": null,
            "languages_offered_in": "interpretation services; English, Korean, Mandarin Chinese, Spanish",
            "notes": null,
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.2552414,
            37.4784326
            ],
            "type": "Point"
        },
        "id": 4
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Menlo Medical Clinic",
            "address": "321 Middlefield Road, Menlo Park, CA 94025",
            "county": "San Mateo",
            "website": "https://stanfordhealthcare.org/medical-clinics/menlo-medical-clinic.html",
            "abortion": "abortoin procedure through 23 weeks, 6 days; pill through 12 weeks, 0 days",
            "birth_control": "birth control pill\nimplant (Nexplanon)\nIUD\nnon-hormonal/copper IUD\nhormonal IUD\nbirth control shot (Depo-Provera)\nsterilization\ntubal ligation (\"getting your tubes tied\")",
            "emergency_contraception": "emergency contraception (EC)\r\nPrescription EC pill (ella)\r\nOver-the-counter EC pill",
            "gender_affirming_care": null,
            "hiv_services": null,
            "mental_health": null,
            "std_testing_and_treatment": "HIV",
            "sexual_and_reproductive_concerns": null,
            "iud_insertion_pain_management": "non-hormonal/copper IUD\r\nhormonal IUD",
            "vaccines": null,
            "wellness_and_preventive_care": null,
            "languages_offered_in": "interpretation services; english, spanish",
            "notes": null,
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.1685042,
            37.4562866
            ],
            "type": "Point"
        },
        "id": 5
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Concord Health Center",
            "address": "2185 Pacheco Street\nConcord, CA 94520",
            "county": "Contra Costa",
            "website": "https://www.plannedparenthood.org/health-center/california/concord/94520/concord-health-center-3269-90200",
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
            "coordinates": [
            -122.0347415,
            37.97905799999999
            ],
            "type": "Point"
        },
        "id": 6
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Walnut Creek Health Center",
            "address": "1357 Oakland Blvd.\nWalnut Creek, CA 94596",
            "county": "Contra Costa",
            "website": "https://www.plannedparenthood.org/health-center/california/walnut-creek/94596/walnut-creek-health-center-2571-90200",
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
            "coordinates": [
            -122.0705378,
            37.8978575
            ],
            "type": "Point"
        },
        "id": 7
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Oakland Health Center",
            "address": "1400 Broadway\nOakland, CA 94612",
            "county": "Alameda",
            "website": "https://www.plannedparenthood.org/health-center/california/oakland/94612/oakland-health-center-21934-90130",
            "abortion": "Abortion pill up to 11 weeks, in-clinic abortions up to 20 weeks",
            "birth_control": null,
            "emergency_contraception": "Emergency contraception pill (morning after pill) ",
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
            "coordinates": [
            -122.2709468,
            37.8043923
            ],
            "type": "Point"
        },
        "id": 8
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "El Cerritto Health Center",
            "address": "280 El Cerrito Plaza\nEl Cerrito, CA 94530",
            "county": "Alameda",
            "website": "https://www.plannedparenthood.org/health-center/california/el-cerrito/94530/el-cerrito-health-center-3940-90200",
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
            "coordinates": [
            -122.2983939,
            37.8992575
            ],
            "type": "Point"
        },
        "id": 9
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Napa Health Center",
            "address": "935 Trancas Street Unit 4D\r\nNapa, CA 94558",
            "county": "Napa",
            "website": "https://www.plannedparenthood.org/health-center/california/napa/94558/napa-health-center-2702-90200",
            "abortion": "Abortion pill up to 11 weeks",
            "birth_control": "EC pills, Birth Control Implant, IUD, birth control patch, birth control pill, NuvaRing, birth control shot, birth control sponge, cervical caps, condoms, diaphragm, spermicide and gel(phexxi)",
            "emergency_contraception": "emergency contraception pills, IUD as emergency contraception",
            "gender_affirming_care": "Hormone therapy\r\nSurgery referrals\r\nEducation\r\nResources",
            "hiv_services": "HIV testing\r\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "testing and treatment for Chlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich) / Condoms\nHepatitis B vaccine (first dose)\nHPV vaccine for prevention",
            "sexual_and_reproductive_concerns": "Jock itch\r\nSexual health concerns, Checkups for reproductive/sexual health concerns\r\nFibroids\r\nInfertility support and referral",
            "iud_insertion_pain_management": "IUD offered",
            "vaccines": "Hepatitis B vaccine\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
            "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test), menopause treatment",
            "languages_offered_in": "English, Spanish",
            "notes": "Insurance accepted: Anthem Blue Cross\r\nBlue Shield of California\r\nContra Costa Health Plan\r\nOscar Health Plan of California\r\nPartnership Health Plan of CA",
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.294775,
            38.3228422
            ],
            "type": "Point"
        },
        "id": 10
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Planned Parenthood- Vallejo Health Center",
            "address": "303 Sacramento St, Vallejo CA 94590",
            "county": "Solano",
            "website": "https://www.plannedparenthood.org/health-center/california/vallejo/94590/centro-de-salud-vallejo-2699-90200?utm_campaign=vallejo-health-center&utm_medium=organic&utm_source=local-listing",
            "abortion": "depending on the stage of pregnancy they provide an abortion pill up to 11 weeks and 0 days after 1st menstrual period\nAbortion pill is by appointment only\n",
            "birth_control": "birth control implant (Nexplanon)\nIUD\nEmergency contraception pill\nBirth control pill\nBirth control patch\nBirth control shot \nBirth control ring (Nuva Ring)",
            "emergency_contraception": "Emergency contraception pill (morning after pill) ",
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
            "coordinates": [
            -122.259051,
            38.0997068
            ],
            "type": "Point"
        },
        "id": 11
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Fairfield Health Center",
            "address": "1325 Travis Blvd. #CFairfield, CA 94533",
            "county": "Solano",
            "website": "https://www.plannedparenthood.org/health-center/california/fairfield/94533/fairfield-health-center-2700-90200",
            "abortion": "abortion pill up to 11 weeks, in-clinic abortion up to 18 weeks",
            "birth_control": "Birth Control implantIUD, Birth control patchBirth Control pillBirth control ring (NuvaRing)Birth Control shot, Birth control spongeCervical capCondomsDiaphragmSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraception pillsIUD as emergency contraception",
            "gender_affirming_care": "Surgery referrals, education, resources",
            "hiv_services": "HIV testingHIV treatment support and referrals",
            "mental_health": "available",
            "std_testing_and_treatment": "testing and treatment for ChlamydiaGenital wartsGonorrheaHerpesSyphilisTrichomoniasis (trich) / CondomsHepatitis B vaccine (first dose)HPV vaccine for prevention",
            "sexual_and_reproductive_concerns": "Jock itchSexual health concerns, Checkups for reproductive/sexual health concernsFibroidsInfertility support and referral",
            "iud_insertion_pain_management": "IUD offered",
            "vaccines": "Hepatitis B vaccineHepatitis B vaccine (first dose)HPV vaccine",
            "wellness_and_preventive_care": "Abnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)Chest/breast cancer screening and referralCervical cancer screening (HPV/Pap test), menopause treatment",
            "languages_offered_in": "English, Spanish",
            "notes": "Insurance accepted: Anthem Blue CrossBlue Shield of CaliforniaContra Costa Health PlanOscar Health Plan of CaliforniaPartnership Health Plan of CA",
            "pregancy_testing": "null",
            "payment_information": "null",
            "prenatal_and_postpartum_services": "null"
        },
        "geometry": {
            "coordinates": [
            -122.0519842,
            38.2576276
            ],
            "type": "Point"
        },
        "id": 12
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "San Francisco Health Center",
            "address": "1522 Bush Street\r\nSan Francisco, CA 94109",
            "county": "San Francisco",
            "website": "https://www.plannedparenthood.org/health-center/california/san-francisco/94109/san-francisco-health-center-3997-90200",
            "abortion": "abortion pill up to 11 weeks, in-clininc abortion up to 18 weeks",
            "birth_control": "Birth Control implant\nIUD, Birth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot, Birth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraceptions,IUD as concraception",
            "gender_affirming_care": "Hormone therapy, Surgery referrals, educational resources",
            "hiv_services": "HIV testing\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "Chlamydia\r\nGenital warts\r\nGonorrhea\r\nHerpes\r\nSyphilis\r\nTrichomoniasis (trich)\r\n\r\nCondoms\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
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
            "coordinates": [
            -122.422614,
            37.7886494
            ],
            "type": "Point"
        },
        "id": 13
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Antioch Health Center",
            "address": "3670 Delta Fair Boulevard\r\nAntioch, CA 94509",
            "county": "Contra Costa",
            "website": "https://www.plannedparenthood.org/health-center/california/antioch/94509/antioch-health-center-2573-90200",
            "abortion": "abortion pill up to 11 weeks; in-clinic abortion up to 13 weeks and 6 days",
            "birth_control": "Education and lifestyle\nBirth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nLow maintenance\nBirth Control implant\nIUD\nUsed on a schedule\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nUsed every time\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
            "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
            "hiv_services": "HIV testing\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "Testing and Treatment\r\nChlamydia\r\nGenital warts\r\nGonorrhea\r\nHerpes\r\nSyphilis\r\nTrichomoniasis (trich)\r\nSTD/STI Prevention\r\nCondoms\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
            "sexual_and_reproductive_concerns": "Infections and irritations\r\nJock itch\r\nSexual health concerns\r\nReproductive health concerns\r\nCheckups for reproductive/sexual health concerns\r\nFibroids\r\nInfertility support and referral",
            "iud_insertion_pain_management": "IUD",
            "vaccines": "Hepatitis B vaccine\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
            "wellness_and_preventive_care": "Cancer Prevention And Screening\r\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test)\r\nWellness Visits And Support\r\nMenopause treatment\r\nPostpartum visit",
            "languages_offered_in": "Spanish",
            "notes": "Insurance accepted We accept:\r\n\r\nAnthem Blue Cross\r\nBlue Shield of California\r\nContra Costa Health Plan\r\nOscar Health Plan of California\r\nPartnership Health Plan of CA",
            "pregancy_testing": null,
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -121.8441851,
            38.0049497
            ],
            "type": "Point"
        },
        "id": 14
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "San Rafael Health",
            "address": "2 H Street, San Rafael, Ca94901",
            "county": "Marin",
            "website": "https://www.plannedparenthood.org/health-center/california/antioch/94509/antioch-health-center-2573-90200",
            "abortion": "abortion pill up to 11 weeks; in-clinic abortion up to 13 weeks and 6 days",
            "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nVasectomy\nBirth Control implant\nIUD\nBirth control patch\nBirth Control pill\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCervical cap\nCondoms\nDiaphragm\nSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
            "gender_affirming_care": "Hormone therapy\nSurgery referrals\nEducation\nResources",
            "hiv_services": "HIV testing\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHepatitis B vaccine (first dose)\nHPV vaccine",
            "sexual_and_reproductive_concerns": "Infections and irritations\nJock itch\nSexual health concerns\nReproductive health concerns\nCheckups for reproductive/sexual health concerns\nFibroids\nInfertility support and referral",
            "iud_insertion_pain_management": null,
            "vaccines": "\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
            "wellness_and_preventive_care": "Cancer Prevention And Screening\r\nAbnormal Pap test follow-up (Colposcopy, Cryotherapy, LEEP)\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test)\r\nWellness Visits And Support\r\nMenopause treatment\r\nVasectomy",
            "languages_offered_in": "Spanish",
            "notes": "Pregnancy tetsing section is mising from some pp centers",
            "pregancy_testing": "Adoption information and referrals\r\nDiscuss all pregnancy options\r\nPregnancy Dating (Ultrasound)\r\nPregnancy test\r\nFertility and pregnancy planning\r\nInfertility support and referral",
            "payment_information": "Major Credit/Debit Cards. Cash",
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.5384097,
            37.9743646
            ],
            "type": "Point"
        },
        "id": 15
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Virtual Health Center at PPNorCal",
            "address": "California",
            "county": "Contra Costa",
            "website": null,
            "abortion": "abortion pill up to 11 weeks",
            "birth_control": "appointment",
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
            "coordinates": [
            -119.4179324,
            36.778261
            ],
            "type": "Point"
        },
        "id": 16
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Hayward Health Center",
            "address": "1032 A Street Hayward, CA 94541",
            "county": "Alameda",
            "website": "https://www.plannedparenthood.org/health-center/california/hayward/94541/hayward-health-center-4150-90130",
            "abortion": "abortion pill up to 11 weeks",
            "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
            "gender_affirming_care": "\nHormone therapy\nSurgery referrals\nEducation\nResources",
            "hiv_services": "HIV testing\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "Testing and Treatment\nChlamydia\nGenital warts\nGonorrhea\nHerpes\nSyphilis\nTrichomoniasis (trich)\nSTD/STI Prevention\nCondoms\nHPV vaccine",
            "sexual_and_reproductive_concerns": "Infections and irritations\r\nJock itch\r\nSexual health concerns\r\nReproductive health concerns\r\nCheckups for reproductive/sexual health concerns\r\nInfertility support and referral\r\nSexual issues\r\nPremature ejaculation",
            "iud_insertion_pain_management": null,
            "vaccines": "HPV vaccine",
            "wellness_and_preventive_care": "Cancer Prevention And Screening\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test)\r\nTesticular and prostate cancer screening\r\nWellness Visits And Support\r\nMenopause treatment\r\nPostpartum visit",
            "languages_offered_in": "spanish,",
            "notes": null,
            "pregancy_testing": "Pregnancy Testing And Options\r\nAdoption information and referrals\r\nDiscuss all pregnancy options\r\nPregnancy test\r\nPregnancy Planning\r\nFertility and pregnancy planning\r\nInfertility support and referral",
            "payment_information": null,
            "prenatal_and_postpartum_services": null
        },
        "geometry": {
            "coordinates": [
            -122.0834222,
            37.6746302
            ],
            "type": "Point"
        },
        "id": 17
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Mountain View Health Center",
            "address": "2500 California Street\r\nMountain View, CA 94040",
            "county": "Santa Clara",
            "website": "https://www.plannedparenthood.org/health-center/california/mountain-view/94040/mountain-view-health-center-2310-90130",
            "abortion": "abortion pill up to 11 weeks",
            "birth_control": "Birth control counseling\nEmergency contraception pills\nFertility Awareness Methods (FAMs)\nBirth Control implant\nIUD\nBirth control patch\nBirth control ring (NuvaRing)\nBirth Control shot\nBirth control sponge\nCondoms\nSpermicide and Gel (Phexxi)",
            "emergency_contraception": "Emergency contraception pills\nIUD as emergency contraception",
            "gender_affirming_care": "Hormone therapy\nSurgery referrals\nResources",
            "hiv_services": "HIV testing\r\nHIV treatment support and referrals",
            "mental_health": null,
            "std_testing_and_treatment": "STD/STI Services\r\nTesting and Treatment\r\nChlamydia\r\nGenital warts\r\nGonorrhea\r\nHerpes\r\nSyphilis\r\nTrichomoniasis (trich)\r\nSTD/STI Prevention\r\nCondoms\r\nHepatitis B vaccine (first dose)\r\nHPV vaccine",
            "sexual_and_reproductive_concerns": "Infections and irritations\r\nJock itch\r\nSexual health concerns\r\nReproductive health concerns\r\nCheckups for reproductive/sexual health concerns\r\nInfertility support and referral\r\nSexual issues\r\nPremature ejaculation",
            "iud_insertion_pain_management": null,
            "vaccines": "Hepatitis B vaccine\nHepatitis B vaccine (first dose)\nHPV vaccine\nFlu vaccine",
            "wellness_and_preventive_care": "Cancer Prevention And Screening\r\nChest/breast cancer screening and referral\r\nCervical cancer screening (HPV/Pap test)\r\nColon cancer screening\r\nTesticular and prostate cancer screening\r\nPrimary Care Screening\r\nAnemia testing\r\nCholesterol screening\r\nDiabetes screening\r\nHigh blood pressure screening\r\nThyroid screening\r\nWellness Visits And Support\r\nMenopause treatment\r\nPostpartum visit($55 - $128)\r\nSmoking cessation\r\nWellness visit (annual exam, routine check up, etc.)",
            "languages_offered_in": "Spanish, tagalog, hindi",
            "notes": null,
            "pregancy_testing": "Pregnancy Testing And Options\nAdoption information and referrals\nDiscuss all pregnancy options\nPregnancy test($15 - $25)\nPregnancy Planning\nFertility and pregnancy planning\nInfertility support and referral",
            "payment_information": null,
            "prenatal_and_postpartum_services": "Miscarriage And Postpartum Care\r\nMiscarriage care and support\r\nPostpartum visit($55 - $128)\r\nOther Services\r\nDiscuss all pregnancy options\r\nPregnancy test($15 - $25)"
        },
        "geometry": {
            "coordinates": [
            -122.1061518,
            37.4034925
            ],
            "type": "Point"
        },
        "id": 18
        },
        {
        "type": "Feature",
        "properties": {
            "clinic": "Hilltop-Richmond Health Center",
            "address": "2970 Hilltop Mall Road #307\r\nRichmond, CA 94806",
            "county": "Contra Costa",
            "website": "https://www.plannedparenthood.org/health-center/california/richmond/94806/hilltop-richmond-health-center-2791-90200",
            "abortion": "Abortion: up to 11 weeks\nIn-clinic: up to 13 weeks and 6 days",
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
            "coordinates": [
            -122.3292435,
            37.97758109999999
            ],
            "type": "Point"
        },
        "id": 19
        }
    ]
  };
  
  onMount(async () => {
    // Only import Leaflet in the browser
    if (browser) {
      L = (await import('leaflet')).default;
      await import('leaflet/dist/leaflet.css');
      
      // Optional: Fetch GeoJSON from file
      // const response = await fetch('/clinics.geojson');
      // clinicData = await response.json();
      
      // Initialize map centered on Berkeley area
      map = L.map(mapContainer).setView([37.8716, -122.2727], 10);
    
    // Add tile layer (OpenStreetMap)
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '© OpenStreetMap contributors',
      maxZoom: 19
    }).addTo(map);
    
    // Custom purple marker icon
    const purpleIcon = L.divIcon({
      className: 'custom-marker',
      html: `<div class="marker-pin"></div>`,
      iconSize: [30, 42],
      iconAnchor: [15, 42],
      popupAnchor: [0, -42]
    });
    
    // Add GeoJSON layer
    L.geoJSON(clinicData, {
      pointToLayer: (feature, latlng) => {
        return L.marker(latlng, { icon: purpleIcon });
      },
      onEachFeature: (feature, layer) => {
        const props = feature.properties;
        
        // Build services list
        const services = [];
        if (props.abortion) services.push('Abortion');
        if (props.birth_control) services.push('Birth Control');
        if (props.emergency_contraception) services.push('Emergency Contraception');
        if (props.gender_affirming_care) services.push('Gender-Affirming Care');
        if (props.hiv_services) services.push('HIV Services');
        if (props.mental_health) services.push('Mental Health');
        if (props.std_testing_and_treatment) services.push('STD Testing & Treatment');
        if (props.sexual_and_reproductive_concerns) services.push('Sexual & Reproductive Concerns');
        if (props.iud_insertion_pain_management) services.push('IUD Insertion Pain Management');
        if (props.vaccines) services.push('Vaccines');
        if (props.wellness_and_preventive_care) services.push('Wellness & Preventive Care');
        if (props.pregnancy_testing) services.push('Pregnancy Testing');
        if (props.prenatal_and_postpartum_services) services.push('Prenatal & Postpartum Services');
        
        const servicesHTML = services.length > 0 
          ? `<div class="services">
              <strong>Services:</strong>
              <ul>${services.map(s => `<li>${s}</li>`).join('')}</ul>
             </div>`
          : '<p class="no-services">No services listed</p>';
        
        // Create popup content
        const popupContent = `
          <div class="clinic-popup">
            <h3 class="clinic-name">${props.clinic || 'Unnamed Clinic'}</h3>
            <p class="clinic-address">${props.address || 'Address not available'}</p>
            ${props.county ? `<p class="clinic-county"><strong>County:</strong> ${props.county}</p>` : ''}
            ${servicesHTML}
            ${props.languages_offered_in ? `<p class="languages"><strong>Languages:</strong> ${props.languages_offered_in}</p>` : ''}
            ${props.payment_information ? `<p class="payment"><strong>Payment:</strong> ${props.payment_information}</p>` : ''}
          </div>
        `;
        
        layer.bindPopup(popupContent, {
          maxWidth: 350,
          className: 'purple-popup'
        });
        
        // Add hover effect
        layer.on('mouseover', function() {
          this.openPopup();
        });
      }
    }).addTo(map);
    
    // Fit map to show all markers
    if (clinicData.features.length > 0) {
      const bounds = L.geoJSON(clinicData).getBounds();
      map.fitBounds(bounds, { padding: [50, 50] });
    }
  }});
  
  // Cleanup on component destroy
  import { onDestroy } from 'svelte';
  onDestroy(() => {
    if (map) map.remove();
  });
</script>

<div class="map-wrapper">
  <div bind:this={mapContainer} class="map-container"></div>
</div>

<style>
  .map-wrapper {
    width: 100%;
    height: 600px;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .map-container {
    width: 100%;
    height: 100%;
  }
  
  /* Custom purple marker styling */
  :global(.custom-marker) {
    background: transparent;
    border: none;
  }
  
  :global(.marker-pin) {
    width: 30px;
    height: 30px;
    border-radius: 50% 50% 50% 0;
    background: #7B3FF2;
    position: absolute;
    transform: rotate(-45deg);
    left: 50%;
    top: 50%;
    margin: -15px 0 0 -15px;
    box-shadow: 0 2px 8px rgba(123, 63, 242, 0.4);
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
  
  /* Purple popup styling */
  :global(.purple-popup .leaflet-popup-content-wrapper) {
    background: linear-gradient(135deg, #7B3FF2 0%, #9D5FF5 100%);
    color: white;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(123, 63, 242, 0.3);
    padding: 0;
  }
  
  :global(.purple-popup .leaflet-popup-tip) {
    background: #7B3FF2;
  }
  
  :global(.purple-popup .leaflet-popup-close-button) {
    color: white !important;
    font-size: 24px !important;
    padding: 8px 12px !important;
  }
  
  :global(.purple-popup .leaflet-popup-close-button:hover) {
    color: #f0e6ff !important;
  }
  
  :global(.clinic-popup) {
    padding: 20px;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Arial, sans-serif;
  }
  
  :global(.clinic-name) {
    margin: 0 0 10px 0;
    font-size: 20px;
    font-weight: 700;
    color: white;
    border-bottom: 2px solid rgba(255, 255, 255, 0.3);
    padding-bottom: 8px;
  }
  
  :global(.clinic-address) {
    margin: 8px 0;
    font-size: 14px;
    opacity: 0.95;
    line-height: 1.5;
  }
  
  :global(.clinic-county) {
    margin: 6px 0;
    font-size: 13px;
    opacity: 0.9;
  }
  
  :global(.services) {
    margin: 15px 0;
    padding: 12px;
    background: rgba(255, 255, 255, 0.15);
    border-radius: 8px;
    backdrop-filter: blur(10px);
  }
  
  :global(.services strong) {
    display: block;
    margin-bottom: 8px;
    font-size: 14px;
    font-weight: 600;
  }
  
  :global(.services ul) {
    list-style: none;
    padding: 0;
    margin: 0;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 6px;
  }
  
  :global(.services li) {
    font-size: 12px;
    padding: 4px 8px;
    background: rgba(255, 255, 255, 0.2);
    border-radius: 4px;
    display: flex;
    align-items: center;
  }
  
  :global(.services li::before) {
    content: '✓';
    margin-right: 6px;
    font-weight: bold;
  }
  
  :global(.no-services) {
    font-style: italic;
    opacity: 0.8;
    font-size: 13px;
  }
  
  :global(.languages),
  :global(.payment) {
    margin: 10px 0;
    font-size: 13px;
    padding: 8px 12px;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 6px;
    line-height: 1.5;
  }
  
  :global(.languages strong),
  :global(.payment strong) {
    display: inline-block;
    margin-right: 6px;
  }
  
  /* Marker hover animation */
  :global(.custom-marker:hover .marker-pin) {
    transform: rotate(-45deg) scale(1.1);
    transition: transform 0.2s ease;
  }
</style>