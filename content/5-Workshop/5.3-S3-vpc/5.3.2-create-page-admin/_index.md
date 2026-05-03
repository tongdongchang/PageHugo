---
title : "Building the admin interface"
date : 2026-05-01
weight : 2
chapter : false
pre : " <b> 4.3.2. </b> "
---


### Objectives

Build the Admin Panel to control all data of the music streaming website. The interface is built with React and Ant Design, including add, edit, and delete functionalities for songs, albums, artists, and users. Only accounts with admin privileges can access this area.

---

### 1. Admin folder structure

Files are organized in the `src/admin/` directory as follows:
src/admin/
├── Admin.jsx # Admin layout (sidebar + content)
├── Album.jsx # Album list, add/edit/delete
├── Artists.jsx # Artist management
├── DetailAlbum.jsx # Album detail (add/remove songs)
├── SliderAdmin.jsx # Navigation sidebar
├── Track.jsx # Track (audio) management
└── Users.jsx # User management

text

All are imported and used within the React Router route tree.

---

### 2. Admin layout (`Admin.jsx` and `SliderAdmin.jsx`)

- **SliderAdmin.jsx** provides the vertical navigation bar on the left, using Ant Design's `Menu`. Main items:
  - Song management (`/admin/tracks`)
  - Album management (`/admin/albums`)
  - Artist management (`/admin/artists`)
  - User management (`/admin/users`)

- **Admin.jsx** uses Ant Design's `Layout`, split into `Sider` (sidebar) and `Content`. It wraps `<Outlet />` to display the corresponding page. Sample code:

```jsx
import { Outlet } from 'react-router-dom';
import { Layout } from 'antd';
import SliderAdmin from './SliderAdmin';

const { Content } = Layout;

const Admin = () => (
  <Layout style={{ minHeight: '100vh' }}>
    <SliderAdmin />
    <Layout>
      <Content style={{ margin: '24px' }}>
        <Outlet />
      </Content>
    </Layout>
  </Layout>
);

export default Admin;
```
### 3. Detailed management pages
#### 3.1. Track management (Track.jsx)
Displays a list of songs in a table (Ant Design Table) with columns: Title, Artist, Album, Duration, Actions.

The Add new button opens a Modal with a Form that allows:

Entering song title, selecting artist and album from available lists

Uploading an audio file (simulated; in a real scenario, the file would be sent to the server after API integration)

Entering duration or auto-detecting it from the file

Each row has:

An Edit button (opens modal pre‑filled with data)

A Delete button with confirmation (Popconfirm)

![track](/images/5-Workshop/5.3-S3-vpc/track.png)


#### 3.2. Album management (Album.jsx)
Album list table includes:

Album name

Artist

Number of songs

Cover image

Add/Edit album via Modal:

Enter album name, select artist

Upload cover image

After creating a new album, you can navigate to DetailAlbum to add songs.

The Delete button shows a warning if the album still contains songs.
![track album](/images/5-Workshop/5.3-S3-vpc/albumadmin.png)

#### 3.3. Album detail (DetailAlbum.jsx)
Receives the album id from the URL.

Displays:

Cover image

Album name

Artist

Two main areas:

List of songs currently in the album (with a remove button)

List of all songs (with search) to add

Can use:

Transfer

Or 2 tables + add/remove buttons

![track albumdetail](/images/5-Workshop/5.3-S3-vpc/detailablum.png)

#### 3.4. Artist management (Artists.jsx)
List table:

Name

Bio (truncated)

Avatar image

Add/Edit modal:

Enter name, bio

Upload image

The Delete button has a confirmation. When deleting, constraints with albums/songs should be checked.
![artist](/images/5-Workshop/5.3-S3-vpc/artist.png)

#### 3.5. User management (Users.jsx)
List table:

Username

Email

Role (Admin/User)

Status (Active/Locked)

Functions:

Change role (Admin/User)

Lock/Unlock account

Delete user (with confirmation)

![user](/images/5-Workshop/5.3.2-admin-frontend/admin-users.png)

### 4. Protecting the Admin route
To prevent regular users from accessing, wrap the admin route with a permission‑checking component:

```
jsx
import { Navigate } from 'react-router-dom';
import { useAuth } from '../contexts/AuthContext';

const AdminRoute = ({ children }) => {
  const { user } = useAuth();
  return user?.role === 'admin' ? children : <Navigate to="/login" />;
};

// Usage
<Route path="/admin" element={<AdminRoute><Admin /></AdminRoute>}>
  ...
</Route>
```
### 5. Results
After completion, the admin area allows full control over the website content through an intuitive, consistent Ant Design interface.

All add, edit, and delete operations provide clear feedback and are safe to use.