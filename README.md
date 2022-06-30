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