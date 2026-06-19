# Hattrick Radar Analysis

## 1. Project Confirmation
**Yes, your understanding is entirely correct.** 
This project is a Hattrick game tool designed to estimate and compare the "real" performance of players. It takes the base skills (Keeper, Defender, Playmaker, Passing, Winger, Scorer, SetPieces) and applies game mechanics modifiers to estimate their effective match contribution. 

The formula found in `radar.php` explicitly applies the following modifiers:
- **Loyalty & Mother Club Bonus**: Added directly to the base skill.
- **Experience**: Logarithmic boost added to the base skill.
- **Form & Stamina**: Applied as multiplicative penalties/bonuses based on power functions.

## 2. Technical Analysis
The application is built using a traditional monolithic architecture:
- **Backend**: PHP. It handles session management, OAuth authentication, and API communication.
- **Frontend**: HTML5, CSS3, and JavaScript. 
- **Libraries & Frameworks**:
  - UI/Styling: Bootstrap 3.2.0, FontAwesome 4.3.0
  - Interactivity: jQuery, Bootstrap-slider, Bootstrap-select
  - Data Visualization: Highcharts (for the polar/radar charts)
- **Database**: **None**. The application is entirely stateless on the server side. It saves the OAuth tokens in browser cookies (`htRadarOauthToken` and `htRadarOauthTokenSecret`) and PHP Sessions to maintain state.

## 3. Implementative Analysis (CHPP Integration)
The core of the application relies heavily on the **CHPP (Certified Hattrick Product Provider)** API. 
- It uses the `PHT` (PHP Hattrick Toolkit) library to abstract the Hattrick API calls.
- Players can be fetched from the user's team (`retrieveTeams.php`) or directly from the transfer market via Player ID (`retrievePlayer.php`).
- The application parses the XML responses from the Hattrick API to extract base skills, form, stamina, experience, and loyalty to instantly populate the UI sliders.

## 4. Self-Hosting Feasibility
**You can easily self-host this website**, and it requires minimal infrastructure.

### What you need to self-host:
1. **A Web Server**: Any server running PHP (e.g., Apache or Nginx). A standard shared hosting plan or a small VPS is more than enough since there is no database.
2. **CHPP Developer Credentials**: This is the most critical step. In the source code (`index.php` and `retrievePlayer.php`), the `CONSUMER_KEY` and `CONSUMER_SECRET` are obfuscated as `*****`. 
   - To make the "Team" and "Market" search features work, you **must** apply for a CHPP Developer key on Hattrick.
   - Once approved, you will receive a Consumer Key and Secret, which you need to insert into the `$config` array in the PHP files.
   - Without these credentials, only the "Manual" input mode will function.

### Setup Steps:
1. Upload the files to your PHP-enabled web server.
2. Obtain your CHPP credentials from Hattrick.
3. Edit `index.php` and `retrievePlayer.php` to include your `CONSUMER_KEY` and `CONSUMER_SECRET`.
4. Ensure the `PHT` library is properly structured in the `PHT/` directory (which it already appears to be).
