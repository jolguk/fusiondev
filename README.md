Power Platform Fusion Development

If you don’t already have one, get a Power Apps account at Business Apps | Microsoft Power Apps This is a 30 day licence which allows you to use premium features such as Dataverse, environments and custom connectors.

Sign on to Azure. 
Create an APIM instance if you don’t already have one:

 
 
You can use the free developer tier for this but be warned that this takes quite a while to provision. Press Review And Create. 

Go to your APIM instance, and click APIs on the left:

 
Click the HTTP section:
 
Select Full rather than Basic and fill out the details, using the Star Wars API  https://swapi.dev/api/    as the web service 
In the Products box select both Starter and Unlimited and leave Gateways at Managed. Press Create.

 
Once created, go to Settings and untick Subscription required and set the API URL suffix to ‘star’, then press Save. 

 

Click on Design and click Add Operation
 
Fill out the GetPeople API as here:
 
Press Save
Press Test and Send
 
You should get a successful 200 response
 
Now export the API to Power Platform; 
Scroll to the left so your API is visible again and then select the Elipsis (3 dots) next to it, and then select Export. (If you are using Azure within the same tenant as Power Platform you could use the Create Power Connector method instead). 
 

Choose OpenAPIv2 (JSON)
 
Now sign onto Power Platform at make.powerapps.com
On the left choose Data then Custom Connectors
 
Choose New Custom Connector at the top right, 
 
Choose Import an OpenAPI file and select the json file you just downloaded. 
 
Press Continue
Add an icon for your connector (an image from your computer) and add a description
 
Press the arrow next to Security at the bottom right
Change the Authentication type on the next screen to no authentication and click the arrow next to Definition
Toggle the Swagger Editor on at the top of the screen and replace the swagger file so it matches the following (change the description entries if you wish and change the host entry to match your own APIM url)

swagger: '2.0'
info: {title: Star Wars API, version: '1.0', description: Power Connector}
host: jofusiondevapim.azure-api.net
basePath: /star
schemes: [https]
securityDefinitions: {}
paths:
  /people/:
    get:
      description: Get characters from the Star Wars universe
      operationId: Getpeople
      summary: GetPeople
      parameters:
      - {name: search, in: query, type: string}
      responses:
        '200':
          description: ''
          schema:
            type: object
            properties:
              count: {type: integer, format: int32, description: count}
              next: {type: string, description: next}
              previous: {type: string, description: previous}
              results:
                type: array
                items:
                  type: object
                  properties:
                    name: {type: string, description: name}
                    height: {type: string, description: height}
                    mass: {type: string, description: mass}
                    hair_color: {type: string, description: hair_color}
                    skin_color: {type: string, description: skin_color}
                    eye_color: {type: string, description: eye_color}
                    birth_year: {type: string, description: birth_year}
                    gender: {type: string, description: gender}
                    homeworld: {type: string, description: homeworld}
                    films:
                      type: array
                      items: {type: string}
                      description: films
                    species:
                      type: array
                      items: {}
                      description: species
                    vehicles:
                      type: array
                      items: {type: string}
                      description: vehicles
                    starships:
                      type: array
                      items: {type: string}
                      description: starships
                    created: {type: string, description: created}
                    edited: {type: string, description: edited}
                    url: {type: string, description: url}
                description: results
  /people/{id}/:
    get:
      description: Get individual characters from Star Wars
      operationId: getpeoplebyid
      summary: GetPeopleById
      parameters:
      - {name: id, in: path, required: true, type: string}
      responses:
        '200': {description: ''}
tags: []

Select create connector
You can test the connector in the dropdown on the left
 
Click New Connection and select your connector, press create
Now to create an app to use this connector
On the left select Apps, new app and Canvas. Give the app a name
Skip the dialogue box which appears. 
On the left select the cylinder symbol, then Add Data
 
Type the name of your custom connector into the box and click on it twice to app it to your app. 
 

Now click on the 3 diamonds on the left to begin editing the UI. 

Click on the Insert menu and select Label. This will add a labelled box of text to the screen. Drag the edges of the box so it becomes a title across the whole top. 
 
On the righthand side is the Properties for this control (the label). Change the text to something like Star Wars Characters and Change the font size, height or anything else you’d like to adjust. Clicking outside the Properties section will save your changes. 
This control is currently called ‘Label1’ Rename it to be TitleLabel
 
Add another label underneath and call it CharacterNameLabel, with ‘Character Name’ as the Text displayed. 
Add 5 more labels underneath for Name, Height, Mass, Eye Colour and Hair Colour as here (you can copy and paste labels): 
 
Now Add a Text Input box where we will type the name of the character to search on. 
 

Delete ‘Text’ from the Default box so it changes to No Value. 
Rename the Text Input Control to be CharacterName (no space)
 
Again from the Insert menu, add a Button to the right of that box, and change its Text to Submit. 
Select the button and type the following into the formula bar at the top:
ClearCollect(characterCollection,StarWarsAPI.Getpeople({search: CharacterName}).results);
 

This means that when we select the button, a Power Apps collection will be created called characterCollection, and this will be populated from the results of running the Getpeople operation from the StarWarsApi connection. 
Now create 5 more labels below the Text Input box and remove their Text values so they each show No Value. 
Next select each one in turn and set its formula to be like this (putting name, mass etc where appropriate): 
 

Now test the app with the Play button (the arrow) at the top right. 

Type a name or part of a name like Luke or r2 in the search box and the rest of that character’s details will populate. 

To save the app, press File, then Save the Publish, then Publish This Version. 



