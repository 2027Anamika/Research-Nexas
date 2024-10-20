# Research-Nexas 🌟🔬📚

**Research-Nexas** is a cutting-edge web application designed to create a seamless connection between **students**, **researchers**, and **stakeholders** within a collaborative research ecosystem. The platform empowers students to log in, upload their research papers, view their uploads, and track their evaluations. 🎓📝 They can also access their profile to see their research details and the **evaluation criteria** set by the stakeholder.

Stakeholders act as research supervisors who can **approve** student submissions and assign papers to the appropriate **faculty members** for evaluation. 👩‍🏫📑 Stakeholders also set evaluation criteria, which they can view on their profile. Faculty members, in turn, can review the assigned papers, provide ratings, and evaluate results based on predefined criteria.

This application creates a **dynamic, feedback-driven environment** where students can improve their research based on faculty evaluations, and stakeholders can ensure quality through customizable criteria. 🌱✨

With **Research-Nexas**, the future of research collaboration is smarter, faster, and more impactful. 💡📈

<p align="center">
  <img src="https://raw.githubusercontent.com/alo7lika/Research-Nexas/refs/heads/main/Research-Nexas%20-%20Application%20Architecture.png" alt="Research-Nexas Application Architecture" width="500"/>
</p>

<img src="https://raw.githubusercontent.com/alo7lika/Research-Nexas/refs/heads/main/Image/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="900">

### This project is now OFFICIALLY accepted for

<div align="center">
  <img src="https://raw.githubusercontent.com/alo7lika/Research-Nexas/refs/heads/main/Image/329829127-e79eb6de-81b1-4ffb-b6ed-f018bb977e88.png" alt="GSSoC 2024 Extd" width="80%">
</div>

<div align="center">
  <img src="https://raw.githubusercontent.com/alo7lika/Research-Nexas/refs/heads/main/Image/hacktober.png" alt="Hacktober fest 2024" width="80%">
</div>

<br>

<img src="https://raw.githubusercontent.com/alo7lika/Research-Nexas/refs/heads/main/Image/212284100-561aa473-3905-4a80-b561-0d28506553ee.gif" width="900">


## 📚 Table of Contents

- [Technical Stack](#technical-stack)
- [Changelog](#changelog)
- [Working](#working)
  - [Student](#student)
  - [Stakeholder](#stakeholder)
  - [Faculty](#faculty)
  - [Result](#result)
- [Prerequisite](#prerequisite)
- [Running the Application](#running-the-application)
- [Future Enhancements / Roadmap](#future-enhancements--roadmap)
- [API Documentation](#api-documentation)
- [License](#license)
- [Contribution](#contribution)
- [Code of Conduct](#code-of-conduct)

## 🛠️ Technical Stack

| **Technology**      | **Description**                                           |
|---------------------|-----------------------------------------------------------|
| **🌐 Frontend**     | HTML, CSS, JavaScript (framework/library not specified)   |
| **🔙 Backend**      | Node.js, Express                                          |
| **💾 Database**     | MySQL                                                    |
| **🧪 Version Control** | Git                                                  |
| **📦 Package Manager** | npm                                                 |
| **💻 Environment**  | Development with VS Code                                |


## 📅 Changelog

### [1.0.0] - 2024-10-15
- Initial release of Research-Nexas.
- User registration and login functionality.
- File upload feature for students.
- Evaluation and rating system for faculty.
- Stakeholder management and evaluation criteria setting.
    
## Working
- Student

  https://github.com/Harshdev098/Research-Nexas/assets/118347330/a26c3b7c-684a-4830-8f11-daf4dac5e8a2

- Stakeholder

  https://github.com/Harshdev098/Research-Nexas/assets/118347330/c6aa876b-095a-4c07-8eea-f402a63bb7bd

- Faculty

  https://github.com/Harshdev098/Research-Nexas/assets/118347330/4106eb28-7931-4adb-9732-a6285ef944c8
  
- Result

  https://github.com/Harshdev098/Research-Nexas/assets/118347330/5b581f5c-5887-4f06-be86-f5fb5cfb68af


## Prerequisite
- MySQL
- NPM & Nodejs


### Running the Application

Follow these steps to run the Research Nexas

- Clone this repository in your computer
- Establishing the database in MySQL Workbench
  - Open MySQL workbench and run these queries
    
     ```
     CREATE SCHEMA user_db;
     use user_db;
     ```
     ```
     create table user_table(
     userid INT auto_increment unique primary key,
     username varchar(60) not null,
     email varchar(80) not null unique,
     password varchar(140) not null unique
     );
     ```
     ```
     create table upload_file_db(
     sno int auto_increment unique primary key,
     userid int not null,
     filename varchar(160) not null unique,
     filepath varchar(220) not null unique,
     status boolean default false,
     fac_mail varchar(80) default null,
     foreign key(fac_mail) references faculty(email) on delete cascade,
     foreign key(userid) references info_table(id) on delete cascade
     );
     ```
     ```
     create table info_table(
     id int unique not null primary key,
     name varchar(70) not null,
     email varchar(80) not null unique,
     col_name varchar(180) not null,
     state varchar(80) not null,
     year int not null,
     course varchar(100) not null,
     foreign key(id) references user_table(userid) on delete cascade
     );
     ```
     ```
     create table stk_holder(
     id int not null auto_increment primary key,
     col_name varchar(180) not null,
     email varchar(80) not null unique,
     password varchar(80) not null unique
     );

     ```
     ```
     create table criteria(
     stk_id int not null unique,
     college varchar(100) not null,
     level1 int not null,
     level2 int not null,
     level3 int not null,
     level4 int not null,
     topic varchar(200) default null,
     level5 int default null,
     foreign key(stk_id) references stk_holder(id) on delete cascade  
     );
     ```
     ```
     create table result(
     resultid int not null auto_increment primary key,
     result float default null,
     userid int not null,
     topic1 int not null,
     topic2 int not null,
     topic3 int not null,
     topic4 int not null,
     topic5 int default null,
     foreign key (userid) references user_table(userid) on delete cascade
     );
     ```
     ```
     create table faculty(
     email varchar(80) not null unique primary key,
     name varchar(60),
     password varchar(120) unique,
     token varchar(130) not null unique
     );
     ```
- Now open code editor(eg. VS Code)
- make a .env file and add the following data to this file
  ```
  DB_HOST=127.0.0.1 //your default host
  DB_USER=root // your user name(by default root)
  DB_PASSWORD=mypassword // your password 
  DB_DATABASE=user_db
  DB_PORT=3306 // databse port
  ACCESS_TOKEN_SECRET = 3a9af42de397cfc9387a06972c28c23a1ac7e9a60fb6dc1f05295bc6057baf500672d4a13db5d04ea84bbc4c5679164a7723f3d49f516bb73dc3df6e3b768c8e
  EMAIL='harsh@gmail.com'   // your email
  MYPASS='yourmailpassword' 
  ```
- You can find `yourmailpassword` for low protected app(developer use) here- https://youtu.be/nuD6qNAurVM
- Now run the following commands in your terminal
  ```
  npm install
  ```
  ```
  cd login-system
  ```
  ```
  nodemon dbServer.js
  ```

- Click the link shown in terminal or open your browser and search for-
  ```
  http://localhost:3000
  ``` 

## 🛣️ Future Enhancements / Roadmap

| **🗓️ Timeline** | **✨ Milestone**                             | **📝 Description**                                                                                                   |
|-----------------|---------------------------------------------|----------------------------------------------------------------------------------------------------------------------|
| **Q4 2024**     | **📊 User Dashboard Improvements**          | Enhance user dashboards with detailed research analytics, including version control for uploaded research papers.    |
| **Q1 2025**     | **💬 Enhanced Faculty-Student Interaction** | Implement real-time chat and discussion boards for faculty-student collaboration on research topics.                 |
| **Q2 2025**     | **🤖 Research Evaluation System Enhancements** | Introduce AI-based evaluation assistance for grading research papers based on predefined criteria.                   |
| **Q3 2025**     | **📱 Mobile App Development**               | Develop and release a mobile version of the Research Nexas platform for both iOS and Android.                       |
| **Q4 2025**     | **🌍 Internationalization and Localization** | Enable multi-language support to expand the platform’s reach to a global audience.                                   |
| **Q1 2026**     | **📚 Publication and Citation Tracking**    | Integrate publication tracking to help users manage where their papers are published and track citations in real-time.|

🚀 **Stay tuned for more updates and exciting features!**

## API Documentation 📚

The Research Nexas application communicates with a backend API to manage various functionalities. Here’s a brief overview of the available API endpoints:

| HTTP Method | Endpoint                    | Description                                             |
|-------------|-----------------------------|---------------------------------------------------------|
| POST        | `/api/register`             | ✍️ Registers a new student or stakeholder.                 |
| POST        | `/api/login`                | 🔐 Logs in a user (student, faculty, or stakeholder).     |
| POST        | `/api/upload`               | 📤 Allows students to upload their research papers.        |
| GET         | `/api/uploads/:userId`      | 📄 Fetches all uploads for a specific user.                |
| POST        | `/api/evaluate`             | ⭐ Submits evaluations and ratings from faculty.           |
| GET         | `/api/criteria/:stkId`      | 📊 Fetches evaluation criteria set by the stakeholder.     |
| POST        | `/api/criteria`             | 🏷️ Sets evaluation criteria by the stakeholder.            |
| GET         | `/api/results/:userId`      | 📈 Fetches evaluation results for a specific user.        |


## License 📝
This project is licensed under the **[MIT License](LICENSE)**. 

## Contribution
Welcome to Research Nexas build for researchers, before contributing to the project please go through our contribution guidelines [Contributing.md](Contributing.md#Opening-a-pull-request). If you have any doubts about guidelines, please open an issue regarding that , we will help for it. **Your PR should follow [Contributing.md](Contributing.md#Opening-a-pull-request) guidelines**.

## Code of Conduct
This project follows [Code of Conduct](Code_of_Conduct.md)




Star ⭐ the project if you like it,working and contributing with us ❤️.


# Big thanks to all the contributors!

| Contributor          | Contributor          | Contributor          | Contributor          |
|----------------------|----------------------|----------------------|----------------------|
| ![Harshdev098](https://github.com/Harshdev098.png) <br> [Harshdev098](https://github.com/Harshdev098) 👨‍💻 | ![Ygowthamr](https://github.com/ygowthamr.png) <br> [Ygowthamr](https://github.com/ygowthamr) 👨‍💻 | ![Ankitha2130](https://github.com/Ankitha2130.png) <br> [Ankitha2130](https://github.com/Ankitha2130) 👩‍💻 | ![Alolika](https://github.com/alo7lika.png) <br> [Alolika Bhowmik](https://github.com/alo7lika) 👩‍💻 |
| ![T Rahul Prabhu](https://github.com/T-Rahul-prabhu-38.png) <br> [T Rahul Prabhu](https://github.com/T-Rahul-prabhu-38) 👨‍💻 | ![Trinetra](https://github.com/trinetra110.png) <br> [Trinetra](https://github.com/trinetra110) 👩‍💻 | ![Rishi](https://github.com/RishiVT2004.png) <br> [Rishi](https://github.com/RishiVT2004) 👨‍💻 | ![Smog Root](https://github.com/smog-root.png) <br> [Smog Root](https://github.com/smog-root) 👨‍💻 |
| ![Harish](https://github.com/harish08102004.png) <br> [Harish](https://github.com/harish08102004) 👨‍💻 | ![Ragini](https://github.com/ragini-gp.png) <br> [Ragini](https://github.com/ragini-gp) 👩‍💻 | ![Bhuvaneswari](https://github.com/KapuluruBhuvaneswariVspdbct.png) <br> [Bhuvaneswari](https://github.com/KapuluruBhuvaneswariVspdbct) 👩‍💻 | ![Shweta](https://github.com/Shweta-1902.png) <br> [Shweta](https://github.com/Shweta-1902) 👩‍💻 |
| ![Soumya](https://github.com/SoumyaU25.png) <br> [Soumya](https://github.com/SoumyaU25) 👩‍💻 | ![Shubham Agarwal](https://github.com/shubhagarwal1.png) <br> [Shubham Agarwal](https://github.com/shubhagarwal1) 👨‍💻 | ![Mrunal Kashid](https://github.com/MrunalKashid02.png) <br> [Mrunal Kashid](https://github.com/MrunalKashid02) 👩‍💻 | ![Siri Chandana](https://github.com/siri-chandana-macha.png) <br> [Siri Chandana](https://github.com/siri-chandana-macha) 👩‍💻 |
| ![Mitul Sonagara](https://github.com/MitulSonagara.png) <br> [Mitul Sonagara](https://github.com/MitulSonagara) 👨‍💻 | ![Dipanita](https://github.com/Dipanita45.png) <br> [Dipanita](https://github.com/Dipanita45) 👩‍💻 | ![Gaurav](https://github.com/Gauravtb2253.png) <br> [Gaurav](https://github.com/Gauravtb2253) 👨‍💻 | ![Anu](https://github.com/Anu27n.png) <br> [Anu](https://github.com/Anu27n) 👩‍💻 |
| ![Ishita](https://github.com/ishita-1305.png) <br> [Ishita](https://github.com/ishita-1305) 👩‍💻 | ![Sudhanshu](https://github.com/Sudhanshu248.png) <br> [Sudhanshu](https://github.com/Sudhanshu248) 👨‍💻 | ![Hamza](https://github.com/Hamza1821.png) <br> [Hamza](https://github.com/Hamza1821) 👨‍💻 | ![Ajay Singh](https://github.com/Ajay-singh1.png) <br> [Ajay Singh](https://github.com/Ajay-singh1) 👨‍💻 |
| ![Archana Singh](https://github.com/archanasingh11.png) <br> [Archana Singh](https://github.com/archanasingh11) 👩‍💻 | ![Tanya Soni](https://github.com/tanya-soni-git.png) <br> [Tanya Soni](https://github.com/tanya-soni-git) 👩‍💻 | ![Kousthub](https://github.com/jvkousthub.png) <br> [Kousthub](https://github.com/jvkousthub) 👨‍💻 | ![Dinkar](https://github.com/Dinkar850.png) <br> [Dinkar](https://github.com/Dinkar850) 👨‍💻 |
| ![Sarthak](https://github.com/Sarthak1970.png) <br> [Sarthak](https://github.com/Sarthak1970) 👨‍💻 | ![Pks](https://github.com/Pks0110.png) <br> [Pks](https://github.com/Pks0110) 👨‍💻 | ![ADeshmukh](https://github.com/ADeshmukh80.png) <br> [ADeshmukh](https://github.com/ADeshmukh80) 👨‍💻 | ![Ash](https://github.com/ash-k121.png) <br> [Ash](https://github.com/ash-k121) 👨‍💻 |
