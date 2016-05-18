---
layout: post
title: Automatic Sleep Tracking
---

<div class="message">
  How I automatically tracked my sleep to my Google calendar.
</div>

I started using the iOS app <a href="//www.sleepcycle.com">Sleep Cycle</a> as an alarm and to track my sleep. After a few weeks of using the app, I looked at my calendar and I couldn't tell when I woke up and went to sleep each night. I wanted to know when I slept-in on weekends, or got up early.

I used **IFTTT**, **Zapier** & **Google Calendar** to connect everything and make the sleep time automatically log to my calendar.

<img src="{{ site.baseurl }}/img/sleep-tracking.png">
<p class="img-caption">Screenshot showing how my sleep is automatically added to my Google calendar.</p>

There are several steps to complete this process, they are as follows:

0. Make an <a href="//ifttt.com/">IFTTT</a> account.

1. Create new IFTTT trigger. Using <a href="//imgur.com/a/03z28">this formula</a>.

2. Download the <a href="//itunes.apple.com/gb/app/up-by-jawbone-track-health/id916240764?mt=8">UP app</a>.

3. To test the IFTTT trigger, go into the UP app and *Track Sleep* for over 2 hours, to force the IFTTT trigger.

4. Edit the IFTTT Google Sheets Spreadsheet to have the sheets that I have in mine <a href="//docs.google.com/spreadsheets/d/1tfuARmQHR5qr0wrssOXsdXpmAqUdGJQPNkImuVN0CFU/edit?usp=sharing">here</a>. Note include 1 value to each sheet row.

5. Create a new Google Sheet script for the IFTTT spreadsheet and add <a href="//pastebin.com/5gEuMWad">this script</a> in it.

6. Now at this point. Your sleep should be automatically tracked and new items post processed and appended to Sheet2. Now to add them to your calendar...

7. Create a <a href="//zapier.com/">Zapier account</a> (I have a whole new account, just for sleep, as this will run everyday). Use <a href="//imgur.com/a/JNf9l">this recipe</a> to append the sleep to your calendar in the correct format.

8. Test everything works by force adding sleep to UP > 2 hours.

9. You (hopefully) should see it appear in your Google calendar after the IFTTT trigger happens and Zapier trigger happens (30m max). You can force IFTTT and Zapier triggers to happen by going to the triggers and pressing run.

​*Google Sheets Script <a href="//pastebin.com/5gEuMWad">found here</a>.*​

​*Google Sheets SpreadSheet <a href="//docs.google.com/spreadsheets/d/1tfuARmQHR5qr0wrssOXsdXpmAqUdGJQPNkImuVN0CFU/edit?usp=sharing">found here</a>.*​
