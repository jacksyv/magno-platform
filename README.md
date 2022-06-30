# Magno Platform

This platform is part of my master's thesis. It allows administration and testing of students using a motion detection test and two variations of a form detection test for use in dyslexia research. The platform is based on the following master theses:

* [Bjørnar Wold's App for Early Detection of Dyslexia](https://ntnuopen.ntnu.no/ntnu-xmlui/handle/11250/2421182)
* [Thea Hove Johansen and Maja Kirkerød's Magno: An Application for Detection of Dyslexia - Dyslexia and Interface Design](https://ntnuopen.ntnu.no/ntnu-xmlui/handle/11250/2454100)
* [Tore Angell Petersen's An Application for Detection of Dyslexia](https://ntnuopen.ntnu.no/ntnu-xmlui/handle/11250/2557938)
* [Fredrik Jenssen's Magno: An Application for Detection of Dyslexia](https://ntnuopen.ntnu.no/ntnu-xmlui/handle/11250/2826619)

The repository for the platform is available at the following URL https://github.com/jacksyvertsen/magno-platform
The repository for the updated tests is available at https://github.com/jacksyvertsen/magno-tests
With a deployed version running at https://magno-test.herokuapp.com/ it is recommended to register a user at Huseby Barneskole as this contains the most test data.

## Usage
**Dependencies**

To run the application you need Node.js and npm installed. After cloning the project, simply run npm install within the directory to install all project dependencies. Afterwards, open a second command line window, and change directory the the server directory and run npm install again to install the server dependencies.

The project uses the following packages:

* [TypeScript](https://www.typescriptlang.org/)
* [Express](https://expressjs.com/)
* [Crypto-js](https://www.npmjs.com/package/crypto-js)
* [MaterialUI](https://mui.com/)
* [Mobx](https://mobx.js.org/README.html)
* [Recharts](https://recharts.org/)
* [uuid](https://www.npmjs.com/package/react-uuid)
* [@azure/cosmos](https://www.npmjs.com/package/@azure/cosmos)
* [universal-cookie-express](https://www.npmjs.com/package/universal-cookie-express)


**Development build**
With dependencies installed, you need to have two command line interfaces open. One pointing to the platform directory, and one pointing to the server directory. To run the platform and server, enter the following command in both CLIs. 

```
npm start
```

The website is hosted at localhost:3000.

**Production build**
To start the build procedure for the platform, run

```
npm run build
```

**Deployment**
To deploy the platform for the first time, create a user at [Heroku](https://dashboard.heroku.com/new-app) and create a new app, choose a fitting name and region. 
After this is done, you need to initiate a new git repository in the server folder, you can follow the instructions given under Deploy using Heroku Git on the page you are redirected to after creating the Heroku App.

Install the Heroku CLI
Download and install the [Heroku CLI](https://devcenter.heroku.com/articles/heroku-command-line).

If you haven't already, log in to your Heroku account and follow the prompts to create a new SSH public key.

```
heroku login
```

Create a new Git repository
Initialize a git repository in a new or existing directory

```
cd magno-platform/server
git init
heroku git:remote -a name-of-your-app-as-set-on-heroku
```

Deploy your application
Commit your code to the repository and deploy it to Heroku using Git.

```
git add .
git commit -am "make it better"
git push heroku master
```

## Integrating new tests

**Back-end**
There are a few steps to integrating new tests

* Build the test, you should end up with a combination of an index.html file, and JavaScript and css files which are usually located in a static folder.
* Navigate to the magno-platform/server/public/tests folder, and create a new folder with a fitting name for your test. Copy the HTML file into this folder.
* Copy the remaining JavaScript and css files directly into the magno-platform/server/public folder

Now for the coding parts of integration.

**

In the magno-platform/server/server.js file you need to add a route to your test, an example is given below of how this is performed.
This is with the HTML file for motion test being located in the magno-platform/server/public/tests/motion folder.

```
const motion_dir = `${__dirname}/public/tests/motion/`;

app.get('/motion', (req, res) => {
  res.sendFile(motion_dir + "index.html", {dotfiles: "allow"});
})
```

An example of how your code might look, replace REPLACE_WITH_NAME_OF_FOLDER with the name you have set for your test folder. Replace REPLACE_WITH_DESIRED_URL_ENDPOINT with your desired url endpoint, as an example,
if this was set to /motion, the url would end up as https://magno-test.herokuapp.com/motion

```
const motion_dir = `${__dirname}/public/tests/REPLACE_WITH_NAME_OF_FOLDER/`;

app.get('/REPLACE_WITH_DESIRED_URL_ENDPOINT', (req, res) => {
  res.sendFile(motion_dir + "index.html", {dotfiles: "allow"});
})
```

**Front-end**
There are a few steps necessary to integrate the test properly with the front-end, e.g. being able to initiate the test from the front-end, and seeing the results in the Student screen.

First you need an image that represents your test, and shows what it looks like, afterwards you need to add this image to the following folder magno-platform/src/files.

Afterwards, open Tests.tsx which is located in magno-platform/src/components/views. Here you will need to add an ActionTestCard, which looks like the following.

```
<ActionTestCard 
    header={props.translation.tests.headerMotion} 
    link={"motion"}
    tooltip={props.translation.tests.tooltip}
    text={props.translation.tests.textMotion} 
    img={MotionDots}
    handleTestClick={openDialog}
    buttonText={props.translation.tests.buttonText}>
</ActionTestCard>
```

For your test it would look like this, where you again replace text located within <> brackets. In addition, you need to import the image you moved into the files folder. You do this at the top of the same file, Tests.tsx

```
import ImageOfTest from '../../files/ImageOfTest.jpg';
```

```
<ActionTestCard 
    header={props.translation.tests.headerNAME_OF_YOUR_TEST} 
    link={"REPLACE_WITH_DESIRED_URL_ENDPOINT"}
    tooltip={props.translation.tests.tooltip}
    text={props.translation.tests.textNAME_OF_YOUR_TEST} 
    img={ImageOfTest}
    handleTestClick={openDialog}
    buttonText={props.translation.tests.buttonText}>
</ActionTestCard>
```



Here you should replace the header text, the link and the text, the link is set directly for the component, whereas the header and text has to be set in the translationNO.tsx file, located in magno-platform/src/components/locales/no/translationNO.tsx, in addition you need to update the Translation.tsx interface located in magno-platform/src/components/locales/Translation.tsx.

For Translation.tsx you should add two lines within tests, headerNAME_OF_YOUR_TEST: string and textNAME_OF_YOUR_TEST: string

```
tests: {
    headerMotion: string,
    textMotion: string,
    headerFixed: string,
    textFixed: string,
    headerRandom: string,
    textRandom: string,
    buttonText: string,
    tooltip: string,
},
```

For translationNO.tsx you should add two lines within tests headerNAME_OF_YOUR_TEST: "Name of your test" and textNAME_OF_YOUR_TEST: "Short description of your test"

```
tests: {
    headerMotion: "Motion Test",
    textMotion: "Magno bevegelsestest er en test som gir en indikasjon på sannsynligheten for at eleven har dysleksi",
    headerFixed: "Form Fixed Test",
    textFixed: "Magno fiksertformtest er en kontrolltest som sjekker om eleven har problemer med synet som ikke skyldes dysleksi",
    headerRandom: "Form Random Test",
    textRandom: "Magno tilfeldigformtest er en kontrolltest som sjekker om eleven har problemer med synet som ikke skyldes dysleksi",
    buttonText: "Start test",
    tooltip: "Starter en test, du får opp et valg av elev før testen starter",
},
```

Alright, well done! You are now able to initiate the test from the front-end! The next step is to show the results in the Students screen.
First you want to add a risk average, or "critical line" which separates a good result from a bad one. For the motion test this is around 20-26.
You add this in Settings.tsx located in magno-platform/src/components/Settings.tsx, just add a key-value pair to the riskAverages dictionary. An example of how this can be done is
shown below, where you reaplce "my_test" and value. If your test has no such risk average, you can set the value to 0.

*Important* 
It is important that this key is equal to the key used when posting the test results to the server. More on this can be found under API endpoint for posting test results. 

```
export const riskAverages = {"motion": 26, "form_fixed": 13, "form_random": 17, "my_test": value}
```

The final step is to add a ChartCard to Student.tsx which is located at magno-platform/src/components/views/Student.tsx, it looks like this.

```
<ChartCard 
    header={props.translation.tests.headerMotion} 
    riskScores={props.store.studentStore.student.tests.motion_test}
    riskAverages={props.store.studentStore.riskAverages}
    translation={props.translation}
    >
</ChartCard>
```

Here you replace

**API endpoint for posting test results**