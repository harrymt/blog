---
layout: post
title: Automatic Sleep Tracking
---

<div class="message">
How I successfully tracked my Sleep to my Google calendar.
</div>

## When I sleep in, I want to know. When I am productive, I want to know.

I started using the iOS app <a href="//www.sleepcycle.com">Sleep Cycle</a> to track my sleep and as an alarm. After a few weeks of using the app, I looked at my calendar and I couldn't tell when I woke up and went to sleep each night. I wanted to know when I slept-in on weekends, or got up early.


<img src="{{ site.baseurl }}/img/sleep-tracking.png">
<p class="img-caption">Screenshot showing how my sleep is automatically added to my Google calendar.</p>


I researched Sleep Cycle and found they did not have an API I could use. I paid the 69 pence for premium to access their online dashboard and found I could access the underlying data. However, this was a very long winded method to retrieving data and **wasn't a sustainable method** - if they changed their front-end codebase, I would need to update my script.

I had previously experimented with tools to connect different services, such as **IFTTT** and **loved** them!

I noticed that Sleep Cycle syncs its data with Apple iOS health. I wanted to access that data and insert it into my calendar.
**IFTTT** doesn't directly integrate with iOS Health, so I had to look around for other services that used that data and integrated with **IFTTT**.

I settled on the Jawbone **UP** app (although I have never owned a Jawbone device) and used **IFTTT**, **Zapier** & **Google Calendar** to connect everything.

## Issues

The most difficult issue was getting the data into the correct format for Google Calendar to process. I was almost regretting my decision to not create my own program, but then I remembered Google Sheets.

I wrote a small script to parse the sleep data into the correct format for Google Calendar to process and I was away!

{% highlight javascript linenos %}

function checkIfNewRow() {

  if(latest_sleep_row != latest_processed_row) {

    // Process the row
    addToFinalSheet();

    // Append to the processed sheet
    sheetLatest.appendRow([latest_sleep]);

  } else {
    // do nothing, as there is nothing new
  }
}


{% endhighlight %}


## Sleep Cycle - Steps

There are several steps to complete the integration process, they are as follows:

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

*Google Sheets Script <a href="//pastebin.com/5gEuMWad">found here</a>.*

*Google Sheets SpreadSheet <a href="//docs.google.com/spreadsheets/d/1tfuARmQHR5qr0wrssOXsdXpmAqUdGJQPNkImuVN0CFU/edit?usp=sharing">found here</a>.*


## Fitbit - Steps

A few months later, I managed to get my hands on a Fitbit Flex and was so happy to find it was MUCH simpler to track my sleep!
I simply used <a href="//ifttt.com/recipes/173925-document-your-daily-activity-in-a-google-spreadsheet">this</a> **IFTTT** trigger and it started logging whenever I slept!
However, using Sleep Cycle was an interesting process where I utilised multiple services to achieve a goal. So I'm glad I did it!
