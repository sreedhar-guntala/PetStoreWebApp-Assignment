*** Settings ***

Library  Selenium2Library
Library  DateTime

*** Variables ***
${BROWSER}  firefox
${CREATE_BUTTON}  id=btn-create
${CURRENT_DATE}  12-04-2016
${NEW_PET_NAME}  Rio Bird
${NEW_PET_STATUS}  All Sold
${ROW_NUMBER_TO_UPDATE}  3
${UPDATED_PET_NAME_TEXT}  Little Mermaid Updated
${UPDATED_PET_STATUS_TEXT}  Only one left Updated
${PET_NAME}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[1]/div/div/form/div[1]/div/input
${PET_STATUS}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[1]/div/div/form/div[2]/div/input
${ROW_NUMBER_PETNAME}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[2]/div/table/tbody/tr[${ROW_NUMBER_TO_UPDATE}]/td[1]/span
${ROW_NUMBER_PETSTATUS}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[2]/div/table/tbody/tr[${ROW_NUMBER_TO_UPDATE}]/td[2]/span
${ROW_NUMBER_PETNAME_VALUE}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[2]/div/table/tbody/tr[${ROW_NUMBER_TO_UPDATE}]/td[1]/input
${ROW_NUMBER_PETSTATUS_VALUE}  xpath=html/body/div[2]/div[2]/div/div/div/div/div[2]/div/table/tbody/tr[${ROW_NUMBER_TO_UPDATE}]/td[2]/input
${HEADER_BANNER_NAVIGATION}  xpath=html/body/div[1]/div/nav/div

*** Test Cases ***

##########################################
#User Story -- US0003: Adding a new pet
#This test is for adding new pet details with Pet Name and Pet Status in PetStore home page
##########################################

User should able to create new pet in PetStore home page
    [Documentation]  This test is for creating new pet with Pet Name and Pet Status details (User Story:US0003)
    [Tags]  Smoke
    Open Browser  http://localhost:3000  ${BROWSER}
    Maximize Browser Window
    Wait Until Element Is Visible  ${CREATE_BUTTON}  timeout=10
    Input Text  ${PET_NAME}  ${NEW_PET_NAME}
    Input Text  ${PET_STATUS}  ${NEW_PET_STATUS}
    Click Button  ${CREATE_BUTTON}
    Scroll Page To Location  0  1000
    sleep  5s  #sleep is used Only for the purpose of giving sufficient time to view UI page actions are visible to user
    Close Browser

##########################################
#User Story -- US0004: Modifying an existing pet
#This test is for modifying the pet details with updated Pet Name and Pet Status in PetStore home page
##########################################

User should able to create new pet in PetStore home page
    [Documentation]  This test is for creating new pet with Pet Name and Pet Status details (User Story:US0003)
    [Tags]  Smoke
    Open Browser  http://localhost:3000  ${BROWSER}
    Maximize Browser Window
    Scroll Page To Location  0  1000
    Wait Until Element Is Visible  ${CREATE_BUTTON}  timeout=10
    Click Element  ${ROW_NUMBER_PETNAME}
    Input Text  ${ROW_NUMBER_PETNAME_VALUE}  ${UPDATED_PET_NAME_TEXT}
    Press Key  ${ROW_NUMBER_PETNAME_VALUE}  \\09
    Click Element  ${ROW_NUMBER_PETSTATUS}
    Input Text  ${ROW_NUMBER_PETSTATUS_VALUE}  ${UPDATED_PET_STATUS_TEXT}
    #Scroll Page To Location  0  300
    #Click Element  ${PET_NAME}
    #Press Key  ${THIRD_ROW_PETSTATUS_VALUE}  \\10
    #Press Key  ${ROW_NUMBER_PETSTATUS_VALUE}  \\13
    sleep  5s  #sleep is used Only for the purpose of giving sufficient time to view UI page actions are visible to user
    Close Browser

#################################################
#User Story -- US0001: Viewing the current date
#Documentation  This test is for verifying the current date display in PetStore home page
#################################################

User must view the current date in PetStore home page
    [Documentation]  This test is for verifying the current date display in PetStore home page
    [Tags]  Smoke
    Open Browser  http://localhost:3000  ${BROWSER}
    Maximize Browser Window
    Wait Until Page Contains  Petstore webapp
    Wait Until Element Is Visible  ${CREATE_BUTTON}  timeout=10
    Element Should Contain  ${HEADER_BANNER_NAVIGATION}  Hello stranger, today\'s date is :
    Element Should Contain  ${HEADER_BANNER_NAVIGATION}  ${CURRENT_DATE}

    sleep  5s  #sleep is used only for the purpose of giving sufficient time to view UI page actions are visible to user
    Close Browser


*** Keywords ***
Scroll Page To Location
    [Arguments]  ${x_location}  ${y_location}
    Execute Javascript  window.scrollTo(${x_location},${y_location})
