---
title: "Week 3 Worklog"
date: 2026-03-23
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
---

### Week 3 Objectives

* Build the main user interface for the music streaming website using React.
* Complete the following pages: Home, Register, Login, Album, Playlist, Music Player Bar, Search, and MV (Music Video) view.
* Create a seamless frontend skeleton, ready to connect with the Django backend.

### Detailed Task Schedule

| Day | Task | Start Date | Completion Date | Reference Material |
| --- | ---- | ---------- | --------------- | ------------------ |
| 2   | - Initialize the React project with Vite, install React Router, set up folder structure <br> - Build the common layout (Header, Footer, Main Container) <br> - Design the Home page: banner, suggested songs list, featured artists (using mock data) | 03/23/2026 | 03/23/2026 | React Docs, React Router Docs |
| 3   | - Create Register and Login pages with forms and basic validation <br> - Integrate React Hook Form for form management <br> - Style auth pages, handle error and loading states | 03/24/2026 | 03/24/2026 | React Hook Form Docs, CSS Modules |
| 4   | - Build the Album detail page: display album info, song list, cover image <br> - Build the Playlist page similar to album, with add/remove song functionality (mock) <br> - Connect data using mock JSON files | 03/25/2026 | 03/25/2026 | React Context API, JSX |
| 5   | - Develop the Music Player Bar (fixed at bottom): play/pause, next/prev, progress bar, volume control <br> - Create the Search interface: input for song/artist, display results as a list <br> - Manage global state for the current song using Context | 03/26/2026 | 03/26/2026 | React Context API, Web Audio API |
| 6   | - Build the MV (Music Video) page: embed a video player (ReactPlayer), show MV details, related MVs list <br> - Review all pages for responsive design on mobile/tablet <br> - Write Week 3 report | 03/27/2026 | 03/27/2026 | ReactPlayer Docs, Responsive Design |

### Week 3 Outcomes

* Completed the basic frontend interface for the entire core flow of the music streaming website.
* Home page successfully displays content suggestion sections, an attractive banner, and clear navigation.
* Register and Login pages have complete forms, client-side validation, and a user-friendly interface.
* Album and Playlist pages:
  * Show detailed collections of songs, cover images, and descriptive info.
  * Allow intuitive add/remove of songs in a playlist (mock).
* Music Player Bar:
  * Controls playback with basic buttons, a progress bar, and volume adjustment.
  * Synchronizes the current song state across the entire app.
* Search interface works, filters results by keyword, and displays them quickly.
* MV page plays videos, has a clear layout, and is ready to receive real data from the backend.
* The entire UI has undergone basic responsive checks, ready for API integration and advanced feature development in the next week.