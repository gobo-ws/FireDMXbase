## FireDMXbase – DMX over Internet

This solution allows you to control DMX lighting remotely by using Firebase as a secure bridge, with no need for open incoming ports or a VPN.

---

### Prerequisites

- Two devices (e.g., Raspberry Pi), one acting as the sender and one as the receiver
- Internet access with outbound HTTPS (port 443), which is typically open on most networks
- [Node-RED](https://nodered.org) installed on both devices
- [@gogovega/node-red-contrib-firebase-realtime-database](https://flows.nodered.org/node/@gogovega/node-red-contrib-firebase-realtime-database) installed on both devices
- [OLA](https://www.openlighting.org/ola/) installed on both devices, with at least one active and configured DMX universe on each device (both sender and receiver)

- [FireDMXbase Node-RED flow](firedmxbase.json) imported into Node-RED

---

### Installation


#### 1. Create a Firebase Account
- Go to [Firebase](https://firebase.google.com/) and sign up for a free account.
- The **Spark Plan** is free and sufficient for most small projects.

#### 2. Create a Realtime Database
- In the Firebase Console, create a new project.
- Navigate to **Build → Realtime Database** and create a new database instance.

#### 3. Enable Anonymous Authentication
- In the Firebase Console, go to **Build → Authentication → Sign-in method**.
- Enable **Anonymous Authentication**.
- Note your **API key** (found in your project settings) for use in your application.

#### 4. Set Up Firebase Security Rules
- In the Firebase Console, go to **Build → Realtime Database → Rules**.
- Set your security rules. For example:

    ```json
    {
      "rules": {
        ".read": true,           // Anyone can read
        ".write": "auth != null" // Only authenticated users can write
      }
    }
    ```

    This allows public read access, but restricts write access to authenticated users.

---

#### 5. Set Up the Node-RED Flow

- Install the sender part of the Node-RED flow on the sending device and the receiver part on the receiving device.
- Edit the Firebase settings, the OLA IP/hostname and the universe in the flow as needed.

---

#### Limitations

- **Latency:** This solution relies on cloud communication, which introduces some latency compared to direct DMX or local network protocols. While it is suitable for remote control, it may not be ideal for time-critical or high-frequency DMX applications.
- **Internet Dependency:** Both sender and receiver devices require a stable Internet connection at all times.
- **Firebase Free Tier Limits:** The free Spark Plan has limits on the number of simultaneous connections, data throughput and write operations per day. For larger or more demanding installations, consider upgrading to a paid plan.

---
