# Sending Notifications

***

### **Sending Notifications with Solflare Wallet**

Apps that want to leverage the Solflare Wallet notification protocol can easily integrate notifications through a user-friendly **Notification Dashboard** or directly through **API endpoints** for more customized business flows.

#### **Access to the Notification Dashboard**

When you integrate with Solflare Wallet, your app will be granted access to a **Notification Dashboard**, where you can:

* **View subscribed public keys**: Track users who have opted in to receive notifications from your app.
* **Manage your casts**: Create, schedule, and send notifications to your users.
* **Monitor general statistics**: Keep an eye on metrics like delivery rates, engagement, and opt-out rates.

#### **Two Types of Notifications: Broadcast vs. Unicast**

There are two primary types of notifications you can send through Solflare:

1. **Broadcast Notifications**:
   * These notifications are sent to all public keys that are subscribed to your app.
   * Broadcast notifications are **not sent immediately**. They undergo a **review process** before being sent to users to ensure compliance with guidelines.
2. **Unicast Notifications**:
   * These are more targeted notifications, sent to a **single public key** (user) that is subscribed to your app.
   * Unicast notifications are sent **immediately** once they are created.

#### **Creating a Cast: Notification Fields**

When creating a notification (called a "cast"), there are several fields you can include. Here’s a breakdown of the fields and their requirements:

| **Field**             | **Mandatory** | **Notes**                                                                            |
| --------------------- | ------------- | ------------------------------------------------------------------------------------ |
| **Title**             | Yes           | The title of the notification.                                                       |
| **Body**              | Yes           | The main content of the notification.                                                |
| **Icon**              | Yes           | A small icon, visible only on web.                                                   |
| **Image**             | No            | A larger image, visible only on mobile.                                              |
| **Action URL**        | No            | A URL that the user will be directed to when they click the notification (web only). |
| **Platform**          | Yes           | Specifies the platform for which the notification is intended (e.g., web, mobile).   |
| **Cast Time**         | Yes\*         | For broadcast notifications, you must specify when to send the notification.         |
| **Topic**             | Yes           | The topic of the notification, helping categorize it.                                |
| **Target Public Key** | Yes\*         | Required for unicast notifications to target a specific user.                        |

#### **Notification Topics**

Notifications are categorized into three **default topics**. These topics help users manage their preferences and decide which types of notifications they want to receive. Users can opt-out of specific topics if they wish.

**1. General**

* **Purpose**: Used for marketing, promotions, and general announcements.
* **Example**: "New features are now available on the app!"

**2. Security**

* **Purpose**: Used for critical security-related updates, such as warnings about potential vulnerabilities or suspicious activities.
* **Example**: "Your account has been accessed from a new device."

**3. Transactional**

* **Purpose**: Targeted notifications about specific events or transactions that involve individual users.
* **Example**: "You have successfully completed a transaction."

#### **How Notifications Work**

**Sending Notifications via the Dashboard:**

* Use the **Notification Dashboard** to easily send and manage both broadcast and unicast notifications. You can configure the title, body, image, and other fields, and set the delivery time or targeting options.

**Sending Notifications via API:**

* For more advanced integrations, you can use the **Solflare API** to send notifications programmatically. This allows your app to trigger notifications based on user actions or other events in your business flow.

#### **Summary**

* **Notification Dashboard**: Manage notifications, view subscribed users, and monitor stats.
* **API Integration**: For custom notification workflows, integrate the Solflare notification API.
* **Two Notification Types**: Broadcast (sent to all subscribers) and Unicast (targeted, sent to one user).
* **Notification Fields**: Includes title, body, icon, image, and action URL.
* **Default Notification Topics**: General, Security, and Transactional.
* **Review Process**: Broadcast notifications require approval before being sent to users.

By using Solflare Wallet’s notification protocol, your app can engage users effectively, keep them informed, and create a more personalized experience.
