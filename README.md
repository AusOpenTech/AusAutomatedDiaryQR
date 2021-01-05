# Automated-diary style QR-code checkin apps in Australia

Some suggestions for augmenting existing state-based QR-code checkin processes

By Vanessa Teague, CEO of Thinking Cybersecurity   
  
(I am A/Prof (Adj.) at the ANU, but this project is independent of ANU.)

The idea is to consider whether we can augment Australian venue check-ins with an automated diary-style app like New Zealand's.

This would not remove the legal requirement (in some states) to use the state app - it would provide an additional mechanism by which users could be notified faster without waiting to come to the top of the manual contact-tracing queue.

## Background

When a person scans a QR code at a venue for covid checkin, there are two different possible information flows:

Option 1: the person is invited to upload their name and phone number, along with the venue's name.  This is the norm in Australia, and is automated in some states' official apps. When someone at the venue tests positive, health officials query the database for other patrons and contact them manually.

Option 2: the person's device makes a record of the venue's name or ID (which it gets from the QR code), along with the date and time.  This is called an 'automated diary' and is used in New Zealand and the UK.  Health authorities provide an electronically-accessible list of public exposure sites, which the app regularly queries.  When a person's diary entry matches a public exposure site at the correct time, the app immediately notifies the user.

There are pros and cons for each approach.  Option 1 allows for human-centred contact tracing, where people are notified by a person rather than an app.  It also allows for enforcement or gentler forms of encouragment of quarantine if necessary.  Option 2 allows for almost-immediate notification, which may be significant for disease control during outbreaks when human contact tracers may experience delays.  Also, it may be acceptable to people who do not consent to centralised uploading of their data (the ones who write 'mickey mouse' and enter someone else's phone number).

We do not have to choose between these options - we can do both!

## An independent automated diary app

The most obvious implementation would be a completely independent, open-source app that simply required people to scan the official QR code a second time (after they had used the official app first).  The app would read information identifying the venue and make a diary note.

### Exactly what information would be stored on the device?   (What our app would do)

At a minimum, the diary note needs to include the venue's ID together with the date and time of attendance.  However, there could be problems with ambiguity (different venues with the same name) or imperfect matching (different ways of writing the name).  Hence it would be best to record some unambiguous identifier rather than relying on names.  The simplest would be the whole QR code's text.  Alternatively, Victoria (for example) has a a long base-64-encoded venue ID.  We would also need a manual option for people whose phones couldn't read the QR code, such as Victoria's 6-character ID.

### What information would need to be published on the official list of public exposure sites?  (What we would need from government)

The minimum requirement is some identifier, readable from the QR code, that is unambiguously included with a computer-readable public list of exposure sites.

The human-readable website of exposure sites contains the right information, but in a form that is quite challenging for computers to parse, and which may introduce ambiguity around different spellings of the same name, venues with the same name in different suburbs, etc.  We would therefore ask for some API access to either the  QR code text or some other unique identifier, along with the other information in the human-readable list of exposure sites.  It would probably be feasible (though harder) to extract the information from the human-readable website if it included the necessary unambiguous venue identifier,  (e.g. the 6-digit code in Victoria or the ACT).


## Advantages
The main advantages are:

- Interstate interoperability - one open-source app could simultaneously read information from all participating state government exposure lists; 
- speedy notification - no waiting for a human contact tracer to work through their queue, or relying on a person to check the exposure list website manually - an automated notification would be received within a few minutes of the exposure location being published;   
- the privacy advantages might appeal to some users who refuse to use the official apps - for example, they might write their phone number on paper at a venue and then make their own automated diary note on their device;
- a different mode of notification - people would be seeing a notification from an app already on their phone rather than receiving a phone call from an unknown number.  Of course, we cannot guarantee that they will notice, understand or respond appropriately.


## Alternatives

### Incorporating it into an official app
The same functionality could also be incorporated into any state's official QR-code reading app.
The main advantage is that people would not have to scan the QR code twice.  I cannot think of any disadvantage compared with the current state-based QR-code checkins.

### Using location information instead
An alternative approach is to use a person's location history instead of requiring them to scan the QR code at a venue.  I have avoided this approach because I am interested in the privacy advantages of a design that does not require people to enable location services.  However, this is a valid approach that some people are [already considering](https://twitter.com/samywamy10/status/1346252635016347648?s=20).  It has minimal further privacy loss for those who already enable location services, because it stores the history only on the user's device.

### Adding check-out time

Check-out time could be enabled as easily with either version of the app.  I note that this is already under discussion for some of the state-based apps.


## Limitations and open questions

Although the automated diary style is much better for privacy overall than Option 1, there are still privacy implications to consider, particularly for an adversary who controls, or gains control of, the device.  For some users, a plaintext list of the venues they have visited may not be acceptable.  We need to consider whether the anonymous IDs (such as PIN codes) are sufficient to ameliorate the problem, when they can be easily re-identified, particularly if the venue is listed as an exposure site.  We should also consider whether the diary could be stored encrypted. It might help to look at how the New Zealand or UK apps deal with this challenge.
