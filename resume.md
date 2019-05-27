---
layout: default
title: Resume
---

{% assign data = site.data.resume %}
<div class="content">
  <div class="text-center">
    <h1>{{ data.name }}</h1>
    <p>{{ data.email }} • +6019 5587609 • github.com/{{ data.github }}</p>
  </div>
  <div>
    <h3>Skills</h3>
    <ul>
      <li><strong>Programming Languages</strong>: {{ data.programming_languages }}</li>
      <li><strong>Frameworks</strong>: {{ data.frameworks }}</li>
      <li><strong>DevOps</strong>: {{ data.devops }}</li>
      <li><strong>Languages</strong>: {{ data.languages }}</li>
      <li><strong>Other</strong>: {{ data.other }} </li>
    </ul>

    <h3>Work Experience</h3>
    {% for work in data.works %}
    <p><strong>{{ work.title }}</strong> - {{ work.company }}</p>
      <time>{{ work.timeframe }}</time>
      <div class="sx-text mg-btm-0-5">
        <ul>
          {% for desc in work.descriptions %}
          <li>{{ desc }}</li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}

    <h3>Projects</h3>
    {% for pro in data.projects %}
    <p><strong>{{ pro.title }}</strong> - {{ pro.stack }}</p>
      <div class="sx-text mg-btm-0-5">
        <ul>
          {% for desc in pro.descriptions %}
          <li>{{ desc }}</li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}


    <h3>Education</h3>
    {% for edu in data.educations %}
      <p><strong>{{ edu.title }}</strong> • {{ edu.school }}</p>
      <time>{{ edu.timeframe }}</time>
      <div class="sx-text mg-btm-0-5">
        <ul>
          {% for desc in edu.descriptions %}
          <li>{{ desc }}</li>
          {% endfor %}
        </ul>
      </div>
    {% endfor %}

    <h3>Extracurricular Experience</h3>
      <p><strong>Head of Department of Education</strong> • Sunway Tech Club</p>
      <time>Auguest 2016 - August 2017</time>
      <div class="sx-text mg-btm-0-5">
        <ul>
          <li>Lead the department members in planning and executing education
          related activities.</li>
          <li>Design and prepare content for a series of programming workshops</li>
          <li>Conduct and assist a series of  programming workshops.</li>
          <li>Design T-shirt, Logo and Poster for CityHack 2017 (Hackathon)</li>
          <li>Emcee for Annual General Meeting 2018</li>
        </ul>
      </div>
  </div>
</div>


