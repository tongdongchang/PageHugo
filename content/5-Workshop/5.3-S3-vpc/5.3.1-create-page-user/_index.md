---
title : "Building the user interface"
date : 2026-05-01
weight : 1
chapter : false
pre : " <b> 4.3.1. </b> "
---


### Objectives

Create a complete user interface for the music streaming website, including public pages and shared components such as Header, Footer, and Music Player. After this section, users can browse music, listen to tracks, create playlists (mock), search, and watch music videos.

---

#### 1. Initialize project and install libraries

```bash
npm create vite@latest frontend -- --template react
cd frontend
npm install
npm install react-router-dom react-hook-form @ant-design/icons react-player
npm run dev
```
#### 2. Folder structure
Files inside src/components/ (based on actual list):
```
text
src/components/
├── Alert.jsx
├── Footer.jsx
├── GetToken.jsx
├── Head.jsx
├── Home.jsx
├── Login.jsx
├── Main.jsx
├── MusicPlayer.jsx
├── PayPal.jsx
├── PlayList.jsx
├── PlayVideoMusic.jsx
├── Register.jsx
├── Search.jsx
├── Slider.jsx
└── UserPlaylist.jsx
```
#### 3. Routes and Main Layout (Main.jsx)
Main.jsx acts as the common layout, containing the Header, Footer, and embedding <Outlet /> for page content.
```
jsx
import { Outlet } from 'react-router-dom';
import Head from './Head';
import Footer from './Footer';
import MusicPlayer from './MusicPlayer';

const Main = () => (
  <>
    <Head />
    <main style={{ minHeight: '80vh' }}>
      <Outlet />
    </main>
    <Footer />
    <MusicPlayer />
  </>
);

export default Main;
In App.jsx, configure routes for the user-facing part:
```
```
jsx
<Route path="/" element={<Main />}>
  <Route index element={<Home />} />
  <Route path="login" element={<Login />} />
  <Route path="register" element={<Register />} />
  <Route path="playlist/:id" element={<PlayList />} />
  <Route path="my-playlists" element={<UserPlaylist />} />
  <Route path="search" element={<Search />} />
  <Route path="mv/:id" element={<PlayVideoMusic />} />
</Route>
```
#### 4. Main components
### 4.1. Header (Head.jsx)
Navigation bar containing the logo, menu items (Home, Search, My Playlists), and a login/register button or avatar.

### 4.2. Home (Home.jsx)
Displays a banner (Slider.jsx), featured songs, artists, and albums. Data is loaded from mock JSON files.

### 4.3. Slider (Slider.jsx)
An image/banner carousel component; can use pure CSS or the Swiper library.

### 4.4. Login & Register (Login.jsx, Register.jsx)
Login/registration forms built with react-hook-form and basic validation. After submission, the token is stored in localStorage via GetToken.jsx.

### 4.5. Search (Search.jsx)
A search box that filters songs, artists, and albums from mock data.

### 4.6. PlayList & UserPlaylist (PlayList.jsx, UserPlaylist.jsx)
View details of a playlist and manage the user's own playlists (add, delete).

### 4.7. Music Player (MusicPlayer.jsx)
A fixed-bottom music player bar using PlayerContext and the <audio> element, with basic playback controls.

### 4.8. Music Video (PlayVideoMusic.jsx)
A page for watching music videos, embedding react-player, and showing video info and related MVs.

#### 5. Results
After completion, the user interface is fully functional with mock data. Reference screenshots:

Homepage interface
![Homepage interface](/images/5-Workshop/5.3-S3-vpc/anhmh.png)

Album page interface
![Album page interface](/images/5-Workshop/5.3-S3-vpc/album.png)

MV playback interface
![MV playback interface](/images/5-Workshop/5.3-S3-vpc/mv.png)

User playlist interface
![User playlist interface](/images/5-Workshop/5.3-S3-vpc/playlist.png)

Login interface
![Login interface](/images/5-Workshop/5.3-S3-vpc/login.png)

Registration interface
![Registration interface](/images/5-Workshop/5.3-S3-vpc/dangky.png)
