# Power Platform Fusion Development

If you don’t already have one, get a Power Apps account at [Business
Apps \| Microsoft Power Apps](https://powerapps.microsoft.com/en-gb/)
This is a 30 day licence which allows you to use premium features such
as Dataverse, environments and custom connectors.

Sign on to Azure.

Create an APIM instance if you don’t already have one:

<img src="./media/image1.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, email Description automatically generated" />

<img src="./media/image2.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, email Description automatically generated" />

You can use the free developer tier for this but be warned that this
takes quite a while to provision. Press Review And Create.

Go to your APIM instance, and click APIs on the left:

<img src="./media/image3.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface Description automatically generated" />

Click the HTTP section:

<img src="./media/image4.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Select Full rather than Basic and fill out the details, using the Star
Wars API <https://swapi.dev/api/> as the web
service<img src="./media/image5.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

In the Products box select both Starter and Unlimited and leave Gateways
at Managed. Press Create.

<img src="./media/image6.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface Description automatically generated" />

Once created, go to Settings and untick Subscription required and set
the API URL suffix to ‘star’, then press Save.

<img src="./media/image7.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application Description automatically generated" />

Click on Design and click Add Operation

<img src="./media/image8.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Fill out the GetPeople API as here:

<img src="./media/image9.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Press Save

Press Test and Send

<img src="./media/image10.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

You should get a successful 200 response

<img src="./media/image11.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application Description automatically generated" />

Now export the API to Power Platform;

Scroll to the left so your API is visible again and then select the
Elipsis (3 dots) next to it, and then select Export. (If you are using
Azure within the same tenant as Power Platform you could use the Create
Power Connector method instead).

<img src="./media/image12.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface Description automatically generated" />

Choose OpenAPIv2 (JSON)

<img src="./media/image13.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Now sign onto Power Platform at make.powerapps.com

On the left choose Data then Custom Connectors

<img src="./media/image14.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Choose New Custom Connector at the top right,

<img src="./media/image15.png" style="width:5.875in;height:1.38542in"
alt="Graphical user interface, application Description automatically generated with medium confidence" />

Choose Import an OpenAPI file and select the json file you just
downloaded.

<img src="./media/image16.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Press Continue

Add an icon for your connector (an image from your computer) and add a
description

<img src="./media/image17.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application Description automatically generated" />

Press the arrow next to Security at the bottom right

Change the Authentication type on the next screen to no authentication
and click the arrow next to Definition

Toggle the Swagger Editor on at the top of the screen and replace the
contents with the contents of the naug.swagger.json file from the github
repository.

Select create connector

You can test the connector in the dropdown on the left

<img src="./media/image18.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application, email Description automatically generated" />

Click New Connection and select your connector, press create.

Select Custom Connectors again on the left, select your new connector
and go to the Test tab. The new connection will now appear in the top
box. Select Test Operation and check you get a 200 response.

Now to create an app to use this connector.

First of all download the FanClub xls file from github and upload it to
your OneDrive.

Then from the make.powerapps.com Home screen, select Excel.

<img src="./media/image19.png" style="width:6.26806in;height:2.45556in"
alt="Graphical user interface, application Description automatically generated" />

Select New Connection and make a Connection to your OneDrive. Select
that connection, and then select the FanClub Excel file

<img src="./media/image20.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application Description automatically generated" />

Then select the MemberList table which appears and Connect

<img src="./media/image21.png"
style="width:6.26806in;height:4.17847in" />The new app will be
instantiated:

<img src="./media/image22.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

First add a connection to your new Custom Connector;

On the left, click on the database symbol, and select Add Data:

<img src="./media/image23.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

Type part of the name of your new connector into the search box, and
click on it when it appears:

<img src="./media/image24.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

Click on it again to create a connection to it and you will see it as a
Data Source alongside the Excel spreadsheet:

<img src="./media/image25.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

Click back onto the 3 diamonds to edit the app

Now you are in Tree View mode. Edit the fields so they show Member,
Member Location, and Member Status rather than what’s there now. Select
BrowseGallery1, and then on the right hand screen click Edit in the
Fields section

<img src="./media/image26.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

Change the Title dropdown to be Member Name and the Body dropdown to be
Member Status

<img src="./media/image27.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application Description automatically generated" />

Now select the arrow to the right of the first member entry, and change
the formula bar to read the following:

ClearCollect(charactersCollection, StarWarsAPI.Getpeople({search: ThisItem.MemberFavoriteCharacter}).results);
Navigate(DetailScreen1);


<img src="./media/image28.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, table, Word Description automatically generated" />

Click on DetailScreen1 on the left (you will probably have to scroll
down to see it).

Create Labels to display details about the Star Wars characters:

Press Insert, then Label to create a Label and move the box to
underneath the existing entries:

<img src="./media/image29.png" style="width:6.26806in;height:4.17847in"
alt="A screenshot of a computer Description automatically generated" />

Copy that label and paste 3 times so you have 4 of them:

Label the top one ‘Name’ by typing into the Text box on the right:

<img src="./media/image30.png" style="width:6.26806in;height:4.17847in"
alt="A screenshot of a computer Description automatically generated" />

Label the 3<sup>rd</sup> one ‘Hair Colour’.

Put borders around the 2<sup>nd</sup> and 4<sup>th</sup> ones by
scrolling down in the properties section and changing the number in
Border from 0 to 4:

<img src="./media/image31.png" style="width:6.26806in;height:4.17847in"
alt="A screenshot of a computer Description automatically generated" />

Also remove the Text from boxes 2 and 4:

<img src="./media/image32.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, application, Word Description automatically generated" />

Now add the formulas to calculate the values for the bordered boxes;

Click onto the first empty box and type the following into the formula
bar:

First(charactersCollection).name

<img src="./media/image33.png" style="width:6.26806in;height:4.17847in"
alt="A screenshot of a computer Description automatically generated" />

Do the same for the other box, substituting Hair_color (NB American
spelling, you will be prompted as the data comes back from the
collection) for Name.

Now you can play the app. Select BrowseScreen1 to return to the home
page, then use the play button on the top tight. Try selecting several
characters, you will probably need to scroll down to find a variety as
the top few will all be Darth Vader

To save your new app, select File, then Save As

<img src="./media/image34.png" style="width:6.26806in;height:4.17847in"
alt="Graphical user interface, text, application Description automatically generated" />

