# Events Plugin for Grav CMS

This is an events plugin that works with [Grav CMS](http://getgrav.org)  0.9.13+.

### Event Frontmatter Example

This plugin process event frontmatter specified in the header in multiple ways. It adds any page found with event frontmatter to `@taxonomy.type = event`. This allows you to build collections based on this taxonomy type.

The `date` of a page will be set to `event.start` automatically if not specified. This allows you to order your events by date.

If the event is a repeating event, pages will be added to the pages collection with the correct dates and times for use throughout the rest of a Grav site. 

```
event:
    start: 01/01/2015 6:00pm
    end: 01/01/2015 7:00pm
    repeat: MTWRFSU
    freq: weekly
    until: 01/01/2020
```

### Dates and Times

The `event.start` and `event.end` dates can be specified using `m/d/y` or `d-m-y` formats along with times.

### Repeating Dates

This plugin supports creating repeating events using `event.repeat`, `event.freq`, and `event.until`. 

`event.repeat` specifies what days you would like for your event to repeat. This can be for Monday through Sunday as specified by MTWRFSU. (**M**onday, **T**uesday, **W**ednesday, Th**U**rsday, **F**riday, **S**aturday, S**U**nday)

`event.freq` can be set to daily, weekly, monthly, or yearly.

`event.until` is a date and time specification like 01/01/2016 12:00am

### Twig Template Example

```
{% set fridayEvents = 
    page.collection({'items':{'@taxonomy.event_repeat':'F'}, 'order':{'by':'date','dir':'asc'}}) %}

<ul>
    {% for event in fridayEvents %}
        <li>
            <a href="{{ event.url }}">{{ event.title }}</a> 
            {{ event.event.start|date('F j, Y') }}
        </li>
    {% endfor %}
</ul>
``` 

### Collection Frontmatter Example

```
collection:
    @items:
```
