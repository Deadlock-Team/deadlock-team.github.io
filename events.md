---
layout: page
title: Events
description: "CTFs that we participated"
permalink: events/
---

<div style="overflow-x:auto;">
<table class="table table-striped">
<thead>
  <tr>
    <th>Colocação</th>
    <th>Evento</th>
    <th>Pontos</th>
  </tr>
</thead>
<tbody>
  {% for event in site.data.events %}
    {% if event.finalized %}
      <tr>
        <td>{{ event.place }}/{{ event.teamstotal }}</td>
        <td><a href="{{ event.ctftimeid }}" target="_blank">{{ event.event }}</a></td>
        <td>{{ event.ctfpoints }}</td>     
      </tr>
    {% endif %}
  {% endfor %}
</tbody>
</table>
</div>
