---
description: user account management
---

# Account

## login

Prompts the user to login if they are not logged in. If an OAuth verifier is not provided, a modal selector will be shown.

```javascript
await torus.login(params);
```

**Parameters**

* `params` - `LoginParams` \(optional\) : The login options. Used to specify a type of login
  * `verifier` - `enum` : The OAuth verifier name. Supported options for verifier are `google` `facebook` `twitch` `reddit` `discord`

**Returns**

* `Promise<string[]>` : Returns a promise which resolves to the Ethereum addresses associated with the user.

**Reference**

```typescript
interface LoginParams {
  verifier?: "google" | "facebook" | "twitch" | "reddit" | "discord";
}
```

**Examples**

```javascript
await torus.login();
```

## logout

Logs the user out of Torus. Requires that a user is logged in already.

```javascript
await torus.logout();
```

**Returns**

* `Promise<void>` : Returns a promise which resolves to void. Rejects if the user is not logged in.

**Examples**

```javascript
await torus.logout();
```

## getUserInfo

Returns the logged-in user's info including name, email, and imageUrl. Only works if the user is logged in. In every `session`, only the first call opens the popup for the user's consent to access this information. All subsequent requests within the session don't trigger the popup.

```javascript
const userInfo = await torus.getUserInfo();
```

**Returns**

* `Promise<UserInfo>` : Returns a promise which resolves to `UserInfo` object.

**Reference**

```typescript
interface UserInfo {
  email: string;
  name: string;
  profileImage: string;
  verifier: string;
  verifierId: string;
}
```

**Examples**

```javascript
const userInfo = await torus.getUserInfo();
```

