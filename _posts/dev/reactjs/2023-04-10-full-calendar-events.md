---
title: "[ReactJS] How to inject events in Full Calendar?"
date: 2023-04-10
categories: [Dev, ReactJS]
tags: [ReactJS]
---

# 1. Create an array with object

Create an array with object having title, start, and end.

```javascript
const events = [
  {
    title: "Event 1",
    start: "2023-04-10T12:00:00",
    end: "2023-04-10T12:00:00",
  },
];
```

# 2. Render the Full Calendar with the created array

```javascript
<FullCalendar plugins={[dayGridPlugin]} events={events} />
```
