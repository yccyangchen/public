---
title: "🙋‍♀️About me"
layout: about
date: 2021-11-06T14:57:28+08:00
hidemeta: true
description: ""
weight:
slug: ""
draft: false # 是否为草稿
comments: true
reward: false
showToc: false # 显示目录
TocOpen: false # 自动展开目录
disableShare: true # 底部不显示分享栏
showbreadcrumbs: false
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---


<!-- ```
class Me:
    def __init__(self):
        self.name = "Chen Yang"
        self.born_year = 1999
        self.MBTI = "ESFP->ENFP"
        self.hometown = "Xianju, Zhejiang, CN"
        self.curr_location = "Darmstadt, Hessen, DE"
        self.grad_school = "TU Darmstadt"
        self.undergrad_school = "ZCMU"
``` -->

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Experience Cards</title>
  <style>
    /* Card container styling */
    .experience-card {
      display: flex;
      flex-direction: row;
      color: #333;
      /* color: red; */
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
      max-width: 1200px;
      margin: 20px;
      overflow: hidden;
    }
    /* Left section styling */
    .card-left {
      background-color: #A9A9A9;
      /* #B0B0B0; */
      /* #A8A29E; */
      color: #ffffff; 
      padding: 30px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      text-align: center;
      width: 200px;
    }
    .card-left h3 {
      margin: 40;
      font-size: 0.8em;
      font-weight: normal;
    }
    .card-left h2 {
      margin: 5px 0 0;
      font-size: 0.8em;
      font-weight: bold;
    }
    /* Right section styling */
    .card-right {
      padding: 20px;
      flex: 1;
    }
    .card-right h3 {
      margin-top: 0;
      font-size: 1.2em;
      font-weight: bold;
      color: #333;
    }
    .card-right p {
      margin: 10px 0 0;
      color: #666;
      font-size: 1em;
    }
    /* Section Heading Styling */
    .section-heading {
      font-size: 1.8em;
      color: #444;
      margin: 40px 0 20px;
      padding-bottom: 5px;
      border-bottom: 2px solid #ddd;
    }
    /* Responsive styling */
    @media (max-width: 600px) {
      .experience-card {
        flex-direction: column;
      }
      .card-left {
        width: 100%;
        text-align: center;
      }
    }
  </style>
</head>
<body>

  <div id="experience-container"></div>

  <!-- Template for Experience Card -->
  <template id="experience-card-template">
    <div class="experience-card">
      <div class="card-left">
        <h3 class="date"></h3>
        <h2 class="company"></h2>
      </div>
      <div class="card-right">
        <h3 class="title"></h3>
        <p class="description"></p>
        <p class="more-info"></p>
      </div>
    </div>
  </template>

  <script>
    // Data array for multiple experience entries with a "type" field
    const experiences = [
      { type: "work", date: "JAN 2024 - PRESENT", company: "COMMERZBANK AG", title: "Working Student", description: "Financial Resource Steering", moreInfo: "" },
      { type: "work", date: "APRIL 2023 - SEPTEMBER 2023", company: "COMMERZBANK AG", title: "Praktikantin", description: " This was a volunteer internship. I was working in Group risk control, liquidity risk where they were currently developing a new website. I contributed in the planning and releasing of the website by analyzing, designing, and implementing it.      {Development of a GUI for an existing Python application to increase usability, including the referring documentation; Development of a shell script to combine the daily log files of a Tomcat server into monthly zip archives and then convert them into an annual archive; Create a Python notebook to automat SQL-based analysis in credit line modeling; Processing of own Jira tickets related to the tasks above within agile formats in a 25-member team using Kanban;}", moreInfo: 'Work certificate can be seen <a href="https://www.google.com" target="_blank">here</a>'},
      { type: "work", date: "OCTOBER 2023 - DECEMBER 2023", company: "Telekooperation Lab, TU Darmstadt", title: "Research assistant", description: "Read papers and replicated privacy policy analysis tools in LinuxBuilt a flashlight application with get location function", moreInfo: "More info will be provided later." },
      { type: "work", date: "APRIL 2022 - SEPTEMBER 2022", company: "Ubiquitous Knowledge Processing Lab, TU Darmstadt", title: "Ethics in NLP Teaching Assistant", description: "Taught tutorials and answered questions in student forum Wrote and developed course materials", moreInfo: "" },
      { type: "study", date: "OCTOBER 2024 - PRESENT", company: "HCI Lab, TU Darmstadt", title: "Master thesis: Fact-checking fake news in VR - a user-based design approach to prevent immersive fake news from spreading", description: "I am developing a fake news prototype in virtual reality which is designed to explore potential fact-checking tool.   ", moreInfo: "Programming language: C++ Tool: Unity" },
      { type: "study", date: "NOVEMBER 2023", company: "Collabothon", title: "Simpilify", description: "In a hackathon with a team of 6, we developed a web application that provide informational stories and AI assistant. User can ask financial related questions and get educational content from stories.", moreInfo: "Programming language: Python, Javascript, HTML, CSS Tool: Vue" },
      { type: "study", date: "NOVEMBER 2023", company: "IVVR", title: "Skateboard game", description: "Organized local events and outreach programs.", moreInfo: "" },
      { type: "study", date: "NOVEMBER 2023 - APRIL 2024", company: "IVVR", title: "bird game 2D", description: "", moreInfo: "" },
      { type: "study", date: "NOVEMBER 2023 - APRIL 2024", company: "TUKI", title: "Start up business idea", description: "In a team of 3 students, we developed an idea to create a new web startup. This was only a pitching project.Our idea is to create the so-called ARP", moreInfo: "" },
      { type: "study", date: "OCTOBER 2022 - APRIL 2023", company: "Master's project", title: "Agile Software Engineering Projekt: KYC", description:`In a team of 5 students, we developed a Know Your Customer platform for a finance company <a href="https://www.neoshare.de/">NEOLOAN AG</a> in Frankfurt.`, moreInfo: 'Programming language: Dart, Javascript<br> Tools: Flutter, Flask, SQLite <br> Technical documentation: <a href="/img/Project_Specification_-_signed_2022-12-21.pdf" download>KYC - Documentation</a> <br> Poster: <img src="/img/KYC.png" alt="KYC Project Poster" width="600" />' },

// moreInfo: 'Work certificate can be seen <a href="https://www.google.com" target="_blank">here</a>'

// <a href="https://www.neoshare.de/">neo</a> 

      { type: "study", date: "APRIL 2022 - OCTOBER 2022", company: "Master's project", title: "Internet Praktikum Telekooperation: Poll", description: "In a team of 5 students, we developed a mobile application for a location-based polling system. Users can create a poll in a specific location.", moreInfo: 'Programming language: Dart, Javascript<br> Tools: Flutter, Flask, SQLite <br> Technical documentation: <a href="/img/PollApp.pdf" download>Poll - Documentation</a> <br> Presentation video: <br>        <video width="640" height="360" controls muted><source src="/img/STG Home Umfragen Video.mp4" type="video/mp4">Your browser does not support the video tag.</video>' },

      // https://git.rwth-aachen.de/maxim.kuznetsov/iptk-2021/-/tree/main?ref_type=headshttps://sharelatex.hrz.tu-darmstadt.de/project/61f81a6f1ca62646c1fe5481

      { type: "study", date: "APRIL 2022 - AUGUST 2022", company: "Master's seminar", title: "Seminar report: Creating Transparency to Raise User's Awareness on Data Collection of Mobile Apps: A Literature Review", description: "The paper is written for the module Schutz von verteilten Infrasturkturen und Netzwerken in a team of 2 students", moreInfo: '<a href="/img/PINSeminar.pdf" download>Read paper</a>' },
      { type: "study", date: "OCTOBER 2021 - APRIL 2022", company: "Master's seminar", title: "Seminar report: Report on SPECTER: Document-level Representation Learning using Citation-informed Transformers", description: "The paper is written for the module Text analytics", moreInfo: '<a href="/img/Text Analytic Chen YANG Report.pdf" download>Read paper</a>' },
      { type: "study", date: "JAN 2020 - JUNE 2020", company: "Bachelor thesis", title: "Bookkeeping app based on Java", description: "Implemented an Android application based on Java and SQLite to help users keeping track of daily expenses. Achieved basic functions such as user register and login, CRDU operations and realized data visualization using Google Charts API.", moreInfo: "Programming language: Java" },
    ];

    // Map for displaying section headings based on type
    const typeMap = {
      work: "Work Experiences",
      education: "Educational Background",
      study: "Projects and Papers",
      volunteer: "Volunteer Experiences"
      // Add other categories here as needed
    };

    const container = document.getElementById('experience-container');
    const template = document.getElementById('experience-card-template').content;

    let lastType = null; // To track the last type added

    experiences.forEach(exp => {
      // Check if we need to add a section heading
      if (exp.type !== lastType) {
        const sectionHeading = document.createElement('h2');
        sectionHeading.className = 'section-heading';
        sectionHeading.textContent = typeMap[exp.type] || "Other Experiences"; // Default if type not found in typeMap
        container.appendChild(sectionHeading);
        lastType = exp.type;
      }

      // Create a new experience card using the template
      const card = document.importNode(template, true);
      card.querySelector('.date').textContent = exp.date;
      card.querySelector('.company').textContent = exp.company;
      card.querySelector('.title').textContent = exp.title;
      card.querySelector('.description').innerHTML = exp.description;
      card.querySelector('.more-info').innerHTML = exp.moreInfo;

      container.appendChild(card);
    });
  </script>

</body>
</html>
