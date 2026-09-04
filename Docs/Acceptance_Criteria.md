# Acceptance Criteria - GG Finder

**Project Name:** GG Finder   
**Version:** 1.0  
**Document Type:** Acceptance Criteria

---

## 1. Introduction

This document defines the acceptance criteria for each feature of the GG Finder mobile application. Each feature is described using the Gherkin format (Given-When-Then) to ensure clear understanding of expected behavior. These criteria will be used to validate that the application meets requirements before final delivery.

---

## 2. User Authentication

### AC-01: User Registration

**As a** new user  
**I want to** create an account  
**So that** I can access the application features  

**Scenario:** Successful registration  
**Given** I am on the registration screen  
**When** I enter valid email, username, and password  
**And** I accept the terms and conditions  
**And** I click the Register button  
**Then** my account is created successfully  
**And** I am redirected to the login screen  
**And** I receive a confirmation message  

**Scenario:** Registration with invalid email  
**Given** I am on the registration screen  
**When** I enter an invalid email format  
**And** I click the Register button  
**Then** an error message "Please enter a valid email" is displayed  
**And** the account is not created  

**Scenario:** Registration with duplicate username  
**Given** I am on the registration screen  
**When** I enter a username that already exists  
**And** I complete all other fields correctly  
**And** I click the Register button  
**Then** an error message "Username already taken" is displayed  
**And** the account is not created  

**Scenario:** Registration with weak password  
**Given** I am on the registration screen  
**When** I enter a password with less than 8 characters  
**And** I click the Register button  
**Then** an error message "Password must be at least 8 characters" is displayed  
**And** the account is not created  

---

### AC-02: User Login

**As a** registered user  
**I want to** log in to my account  
**So that** I can access the application  

**Scenario:** Successful login  
**Given** I have a registered account  
**When** I enter valid username/email and password  
**And** I click the Login button  
**Then** I am authenticated successfully  
**And** I am redirected to the dashboard  
**And** my session is maintained  

**Scenario:** Login with incorrect password  
**Given** I have a registered account  
**When** I enter correct username but wrong password  
**And** I click the Login button  
**Then** an error message "Invalid credentials" is displayed  
**And** I remain on the login screen  

**Scenario:** Login with non-existent account  
**Given** I have not registered  
**When** I enter a username that doesn't exist  
**And** I enter any password  
**And** I click the Login button  
**Then** an error message "Account not found" is displayed  

**Scenario:** Login with empty fields  
**Given** I am on the login screen  
**When** I leave username and password fields empty  
**And** I click the Login button  
**Then** validation errors appear for both fields  
**And** I am not logged in  

---

### AC-03: User Logout

**As a** logged-in user  
**I want to** log out of my account  
**So that** I can end my session  

**Scenario:** Successful logout  
**Given** I am logged into the application  
**When** I click the Logout button  
**Then** my session is terminated  
**And** I am redirected to the login screen  
**And** I cannot access protected features  

---

## 3. Location Services

### AC-04: Location Permission Request

**As a** user  
**I want to** grant location permission  
**So that** the app can find nearby gamers  

**Scenario:** Granting location permission  
**Given** I launch the app for the first time  
**When** the location permission dialog appears  
**And** I click Allow  
**Then** location services are enabled  
**And** the app starts detecting my location  

**Scenario:** Denying location permission  
**Given** I launch the app for the first time  
**When** the location permission dialog appears  
**And** I click Deny  
**Then** an information message appears  
**And** I am redirected to a screen explaining why location is needed  

**Scenario:** Re-enabling permission after denial  
**Given** I previously denied location permission  
**When** I go to app settings and enable location  
**And** I return to the app  
**Then** location services are now enabled  
**And** the app functions normally  

---

### AC-05: GPS Location Tracking

**As a** user  
**I want to** share my location  
**So that** other gamers can find me  

**Scenario:** Location detection when GPS is active  
**Given** I have granted location permission  
**And** GPS is enabled on my device  
**When** I open the app  
**Then** my current location is detected  
**And** my location is updated on the map  
**And** nearby gamers are displayed  

**Scenario:** Location detection when GPS is inactive  
**Given** I have granted location permission  
**But** GPS is disabled on my device  
**When** I open the app  
**Then** an error message "Please enable GPS" is displayed  
**And** I am prompted to enable GPS  

---

### AC-06: Distance Calculation

**As a** user  
**I want to** see how far other gamers are  
**So that** I can choose nearby teammates  

**Scenario:** Accurate distance display  
**Given** I am in Chicago, IL  
**And** another user is in the same city  
**When** I view the nearby gamers list  
**Then** the distance to each gamer is displayed  
**And** distances are accurate within 100 meters  
**And** units are displayed in kilometers  

**Scenario:** Display gamers within 5km only  
**Given** I am viewing the nearby gamers list  
**When** the list loads  
**Then** only gamers within 5km radius are shown  
**And** gamers beyond 5km are not displayed  

---

## 4. Gamer Discovery

### AC-07: Browse Nearby Gamers

**As a** user  
**I want to** see a list of nearby gamers  
**So that** I can find potential teammates  

**Scenario:** Display nearby gamers list  
**Given** I am logged in and location is enabled  
**When** I view the dashboard  
**Then** I see a list of gamers within 5km  
**And** each entry shows: username, game, rank, and status  
**And** users are sorted by distance (closest first)  
**And** online status indicators are visible  

**Scenario:** No nearby gamers found  
**Given** I am logged in and location is enabled  
**But** there are no gamers within 5km  
**When** I view the dashboard  
**Then** a message "No gamers found nearby" is displayed  
**And** I am given the option to expand my search  

**Scenario:** Loading indicator during search  
**Given** I open the dashboard  
**When** the system searches for nearby gamers  
**Then** a loading indicator is displayed  
**And** the list updates when results are ready  

---

### AC-08: Filter and Sort Options

**As a** user  
**I want to** filter and sort nearby gamers  
**So that** I can find specific types of players  

**Scenario:** Filter by online status  
**Given** I am viewing the nearby gamers list  
**When** I select "Available" filter  
**Then** only gamers with "Available" status are shown  
**And** Busy and Offline users are hidden  

**Scenario:** Filter by game  
**Given** I am viewing the nearby gamers list  
**When** I select a specific game  
**Then** only gamers playing that game are shown  
**And** gamers playing other games are hidden  

**Scenario:** Sort by distance  
**Given** I am viewing the nearby gamers list  
**When** I select "Sort by Distance"  
**Then** gamers are sorted from closest to farthest  

**Scenario:** Sort by skill level  
**Given** I am viewing the nearby gamers list  
**When** I select "Sort by Skill Level"  
**Then** gamers are sorted from highest to lowest skill  

**Scenario:** Search by username  
**Given** I am viewing the nearby gamers list  
**When** I type a username in the search bar  
**Then** only matching users are displayed  
**And** results update as I type  

---

## 5. User Profiles

### AC-09: View Gamer Profile

**As a** user  
**I want to** view another gamer's full profile  
**So that** I can decide if I want to play with them  

**Scenario:** Open profile from nearby list  
**Given** I am viewing the nearby gamers list  
**When** I tap on a gamer's entry  
**Then** their full profile is displayed  
**And** profile shows: username, display name, main game, rank  
**And** profile shows: preferred role, win rate, all games  
**And** a "Send Squad Request" button is visible  

**Scenario:** Profile with incomplete information  
**Given** I tap on a gamer with minimal profile data  
**When** their profile opens  
**Then** available information is displayed  
**And** missing fields show "Not specified"  

**Scenario:** Viewing own profile  
**Given** I am logged in  
**When** I tap on my profile  
**Then** my full profile is displayed  
**And** an "Edit Profile" button is visible  

---

### AC-10: Edit Personal Profile

**As a** user  
**I want to** edit my profile  
**So that** I can keep my information up to date  

**Scenario:** Update display name  
**Given** I am on my profile edit screen  
**When** I change my display name  
**And** I click Save  
**Then** my display name is updated  
**And** the change is visible immediately  

**Scenario:** Upload profile picture  
**Given** I am on my profile edit screen  
**When** I upload a new profile picture  
**And** I click Save  
**Then** the picture is uploaded successfully  
**And** my profile picture is updated  

**Scenario:** Update game preferences  
**Given** I am on my profile edit screen  
**When** I add a new game to my profile  
**And** I set rank and role  
**And** I click Save  
**Then** the game is added to my profile  
**And** it appears in my gaming list  

**Scenario:** Remove a game from profile  
**Given** I have games listed on my profile  
**When** I remove a game  
**And** I click Save  
**Then** the game is removed from my profile  
**And** it no longer appears in my gaming list  

---

### AC-11: Add Gaming Preferences

**As a** user  
**I want to** specify my gaming preferences  
**So that** I can find compatible teammates  

**Scenario:** Set main game  
**Given** I have multiple games in my profile  
**When** I select one as my main game  
**And** I click Save  
**Then** the game is marked as my primary game  
**And** it appears prominently in my profile  

**Scenario:** Set preferred role  
**Given** I am editing my game preferences  
**When** I select a preferred role for a game  
**And** I click Save  
**Then** the role is saved for that game  
**And** it appears in my profile  

**Scenario:** Set skill level  
**Given** I am editing my game preferences  
**When** I set a skill level (1-100) for a game  
**And** I click Save  
**Then** the skill level is saved  
**And** it appears in my profile  

---

## 6. Squad Requests

### AC-12: Send Squad Request

**As a** user  
**I want to** send a squad request to another gamer  
**So that** I can invite them to play together  

**Scenario:** Send request successfully  
**Given** I am viewing another gamer's profile  
**When** I click "Send Squad Request"  
**Then** a request is sent to the other user  
**And** I receive confirmation "Request sent successfully"  
**And** the button changes to "Request Pending"  

**Scenario:** Send request with custom message  
**Given** I am viewing another gamer's profile  
**When** I click "Send Squad Request with Message"  
**And** I type a custom message  
**And** I click Send  
**Then** the request with my message is sent  
**And** the recipient sees my message  

**Scenario:** Prevent duplicate requests  
**Given** I have already sent a request to a user  
**When** I try to send another request  
**Then** an error message "Request already sent" is displayed  
**And** the request is not duplicated  

**Scenario:** Prevent self-request  
**Given** I am viewing my own profile  
**When** I try to send a squad request to myself  
**Then** the "Send Squad Request" button is not visible  

---

### AC-13: Receive Squad Request

**As a** user  
**I want to** receive squad requests  
**So that** I can accept or decline them  

**Scenario:** Receive notification for new request  
**Given** Another user sends me a squad request  
**When** I am using the app  
**Then** a push notification is displayed  
**And** the notification shows sender name  
**And** the request appears in my notifications inbox  

**Scenario:** View incoming request  
**Given** I have received a squad request  
**When** I open my notifications  
**Then** I see the request with sender details  
**And** I see Accept and Reject buttons  

**Scenario:** Accept squad request  
**Given** I have an incoming request  
**When** I click Accept  
**Then** the sender is notified of acceptance  
**And** the request status changes to Accepted  
**And** the request is moved to completed  

**Scenario:** Reject squad request  
**Given** I have an incoming request  
**When** I click Reject  
**Then** the sender is notified of rejection  
**And** the request status changes to Rejected  

**Scenario:** Request expires  
**Given** I have an incoming request  
**And** 24 hours have passed  
**When** I open my notifications  
**Then** the request shows as Expired  
**And** I cannot accept or reject it  

---

### AC-14: Manage Squad Requests

**As a** user  
**I want to** manage all my squad requests  
**So that** I can track my gaming invitations  

**Scenario:** View outgoing requests  
**Given** I have sent multiple squad requests  
**When** I navigate to "My Requests"  
**And** I select "Outgoing" tab  
**Then** all my sent requests are displayed  
**And** each shows recipient name and status  

**Scenario:** View incoming requests  
**Given** I have received multiple squad requests  
**When** I navigate to "My Requests"  
**And** I select "Incoming" tab  
**Then** all my received requests are displayed  
**And** each shows sender name and status  

**Scenario:** Cancel pending request  
**Given** I have a pending outgoing request  
**When** I click Cancel  
**Then** the request is cancelled  
**And** the recipient is notified  

**Scenario:** Request history  
**Given** I have accepted and rejected requests  
**When** I navigate to request history  
**Then** I see all completed requests  
**And** each shows final status  

---

## 7. Online Status Management

### AC-15: Set Online Status

**As a** user  
**I want to** set my online status  
**So that** others know if I'm available to play  

**Scenario:** Set status to Available  
**Given** I am logged in  
**When** I select "Available" status  
**Then** my status changes to Available  
**And** I appear as Available in nearby lists  
**And** I am prioritized in search results  

**Scenario:** Set status to Busy  
**Given** I am logged in  
**When** I select "Busy" status  
**Then** my status changes to Busy  
**And** I appear as Busy in nearby lists  
**And** others know I'm currently gaming  

**Scenario:** Set status to Offline  
**Given** I am logged in  
**When** I select "Offline" status  
**Then** my status changes to Offline  
**And** I do not appear in nearby searches  

**Scenario:** Status persists after app restart  
**Given** I set my status to Available  
**When** I close and reopen the app  
**Then** my status remains Available  

---

### AC-16: Auto-Status Update

**As a** user  
**I want to** have my status updated automatically  
**So that** I don't have to manage it manually  

**Scenario:** Auto-available when app is open  
**Given** I have the app open and active  
**When** I am not manually set to Busy  
**Then** my status is automatically Available  

**Scenario:** Auto-offline after inactivity  
**Given** I have the app open  
**When** I have been inactive for 15 minutes  
**Then** my status changes to Offline automatically  

**Scenario:** Auto-online when app returns to foreground  
**Given** I was offline due to app being in background  
**When** I bring the app to foreground  
**Then** my status changes back to Available  

---

## 8. Notifications

### AC-17: Push Notifications

**As a** user  
**I want to** receive push notifications  
**So that** I don't miss gaming opportunities  

**Scenario:** Receive notification for new request  
**Given** Another user sends me a squad request  
**When** I am not actively using the app  
**Then** a push notification appears on my device  
**And** the notification shows sender name and request details  

**Scenario:** Receive notification for accepted request  
**Given** I sent a squad request  
**And** the recipient accepts it  
**When** I am not actively using the app  
**Then** a push notification appears  
**And** the notification shows acceptance message  

**Scenario:** Receive notification for rejected request  
**Given** I sent a squad request  
**And** the recipient rejects it  
**When** I am not actively using the app  
**Then** a push notification appears  
**And** the notification shows rejection message  

---

### AC-18: Notification Management

**As a** user  
**I want to** manage notification preferences  
**So that** I control what notifications I receive  

**Scenario:** Enable/disable notification types  
**Given** I am in notification settings  
**When** I toggle a notification type off  
**Then** I no longer receive those notifications  

**Scenario:** Set quiet hours  
**Given** I am in notification settings  
**When** I set quiet hours from 10PM to 8AM  
**Then** I do not receive notifications during those hours  

---

## 9. Error Handling

### AC-19: Network Errors

**Scenario:** Handle offline mode  
**Given** I am using the app  
**When** I lose internet connection  
**Then** a "No Internet Connection" message is displayed  
**And** previously loaded data is still visible  
**And** actions requiring network are disabled  

**Scenario:** API timeout handling  
**Given** I am making an API request  
**When** the request takes more than 30 seconds  
**Then** a "Request timed out" message is displayed  
**And** I can retry the request  

**Scenario:** Server error handling  
**Given** I am making an API request  
**When** the server returns a 500 error  
**Then** a "Something went wrong" message is displayed  
**And** the error is logged  

---

## 10. Responsive Design

### AC-20: Device Compatibility

**Scenario:** Compatible with iOS devices  
**Given** I am using an iPhone (models 8-14)  
**When** I open the app  
**Then** the app renders correctly  
**And** all features are accessible  

**Scenario:** Compatible with Android devices  
**Given** I am using an Android device (5.0+)  
**When** I open the app  
**Then** the app renders correctly  
**And** all features are accessible  

**Scenario:** Different screen sizes  
**Given** I am using a device with any screen size  
**When** I open the app  
**Then** the layout adapts appropriately  
**And** all content is visible without scrolling (where possible)  

**Scenario:** Different orientations  
**Given** I am using the app  
**When** I rotate my device  
**Then** the layout adjusts to the new orientation  
**And** all content remains accessible  

---

## 11. Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-09-04 | Project Team | Initial document creation |

---

**End of Acceptance Criteria**

*This document defines all acceptance criteria for the GG Finder mobile application.*
