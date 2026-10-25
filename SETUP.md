# Fairlane Rallye Planner on GitHub – with ready-made map data

You need: a computer with a browser, an email address, about 30 minutes for the set-up.
Then GitHub does the heavy work (loading and classifying the map) by itself while you do something else.

## What you end up with
* The planner at an address like `https://YOUR-NAME.github.io/fairlane/` (GPS works there, it does not from a saved file).
* A folder `data` in the same place with the finished classification of your region.
  The phone downloads these small files instead of asking the map servers and calculating on the phone.
  Areas that are not ready are loaded live, exactly as before.

Everything stays public (GitHub Pages are public on the free plan). The files contain only code and OpenStreetMap-derived
road classifications, no personal data. Your own ratings stay in your phone's browser.

---

## Part 1 – Put the planner online (once)

1. Go to **github.com**, click **Sign up**, create a free account.
2. Click **+** (top right) → **New repository**.
   Name: `fairlane`. Choose **Public**. Tick **Add a README file**. Click **Create repository**.
3. **Upload the planner:** click **Add file → Upload files**.
   Rename the planner file on your computer to exactly `index.html` first, then drag it in. Click **Commit changes**.
4. **Switch on the web page:** **Settings** (top row of the repository) → **Pages** (left) →
   under *Build and deployment* choose **Deploy from a branch**, branch **main**, folder **/ (root)** → **Save**.
5. After 1–2 minutes the same page shows *Your site is live at …*. Open that address on your phone in Chrome.

## Part 2 – Add the "robot" that prepares the map data (once)

The robot is a small program that GitHub runs for you. Two text files are needed.

**File 1 – the work program**
1. In your repository click **Add file → Create new file**.
2. In the name box type exactly: `tools/build_tiles.py`
   (typing the slash creates the folder `tools`).
3. Open the file `build_tiles.py` I sent you with any text editor, select all, copy, and paste it into the big text box.
4. Click **Commit changes…** → **Commit changes**.

**File 2 – the start button**
1. **Add file → Create new file**. Name box: `.github/workflows/build-data.yml`
2. Paste the complete content of `build-data.yml` (also sent to you). **Commit changes**.

**Allow the robot to save its results**
1. **Settings → Actions → General**.
2. Scroll to **Workflow permissions**, choose **Read and write permissions**, click **Save**.

## Part 3 – Run it

1. Click **Actions** (top row). If GitHub asks, click *"I understand my workflows, go ahead and enable them"*.
2. Left side: **Build ready-made map data** → button **Run workflow** (right).
3. A small form appears:
   * *Centre of the region*: latitude,longitude – the default is Fürstenfeldbruck / Munich west. Replace it with the place you drive from.
     (Tip: in Google/Apple Maps long-press a place, the numbers appear.)
   * *Radius in km*: start with **50** (about 80 map areas, roughly 1–2 hours).
   * *Stop after minutes*: leave 300.
4. Click the green **Run workflow**. Done – you can close the page. GitHub works in the background.
5. When the line has a green tick, open the repository: there is a new folder **data**. Your planner now uses it.
   (If the green tick is there but the phone does not show "ready-made" after a few minutes, open
   *Settings → Pages* once and click *Save* again so the site refreshes.)

### If it stops half-way
Big regions take longer than GitHub allows in one go (6 hours). The robot stops politely, saves what it finished and
**continues where it stopped** the next time you press *Run workflow*. Press it again until the log says
*"0 failed"* and nothing new is built.

## How to see that it works
In the Explore tab, the grey info line shows **"⚡ 25 areas ready-made (built 2026-10-25)"** after the map has loaded.
Loading is then much faster and uses little mobile data.

## When must the data be rebuilt?
* When I send you a new planner version that changes the classification, I will say so. The page then ignores the old files
  automatically (it compares a version stamp) and loads live again until you press *Run workflow* once more.
  The robot detects the new version itself and rebuilds everything.
* Roads change slowly. Rebuilding every few months is plenty.
* The ready-made data is made for the **1958 Fairlane profile with its standard settings**. If you move the car sliders or
  choose another car, the planner loads live instead (it is slower but always correct).

## If something goes wrong
* **The run turns red:** click it, click the red step, and send me the last 30 lines of text.
  Most likely the public map servers refused GitHub's computers for a while. Just start it again later.
* **Nothing is "ready-made" on the phone:** check the address is the `https://…github.io/…` one (not a downloaded file),
  and that the `data` folder exists in the repository.
* **Repository gets large:** each rebuild adds data to GitHub's history. Rebuild rarely; a region like yours stays well below
  GitHub's limits.

## Licence note
Map data © OpenStreetMap contributors (ODbL). The planner already shows this credit.
