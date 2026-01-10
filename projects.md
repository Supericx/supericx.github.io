---
layout: default
title: Projects
---
{%- include header.html -%}

<article class="projects">
    {%- include back-link.html -%}
    <h2 class="projects__title">My Projects</h2>

    <section class="projects__section">
        <h3>Featured Projects</h3>
        {%- for project in site.data.projects.featured -%}
        <div class="project-card">
            <h4>{{ project.name }}</h4>
            <p>{{ project.description }}</p>
            <p><strong>Tech Stack:</strong> {{ project.tech }}</p>
            <p><strong>Status:</strong> {{ project.status }}</p>
            <p><strong>Key Features:</strong></p>
            <ul>
                {%- for feature in project.features -%}
                <li>{{ feature }}</li>
                {%- endfor -%}
            </ul>
        </div>
        {%- endfor -%}
    </section>

</article>
