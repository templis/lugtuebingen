---
title: Aktuelles
content:
    items:
        '@taxonomy':
            type: event
    order:
        by: date
        dir: asc
    limit: '0'
    pagination: false
process:
    markdown: true
    twig: true
admin:
    children_display_order: collection
---

{% set events =
    page.collection({
        'items':{
            '@taxonomy.type':'event',
            '@taxonomy.event_repeat':['S','U']
        }
    })
    .dateRange(datetools.startOfMonth, datetools.endOfMonth)
    .order('date', 'asc')
%}

<ul>
    {% for event in events %}
        <li class="h-event">
            <a href="{{ event.url }}" class="p-name u-url">{{ event.title }}</a>
            <time class="dt-start" datetime="{{ event.header.event.start|date('c') }}">{{ event.header.event.start|date('F j, Y') }}</time>
        </li>
    {% endfor %}
</ul>