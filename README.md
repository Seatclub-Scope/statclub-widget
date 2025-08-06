# @statclub/widget

A React Native widget package that can be embedded in third-party applications to provide StatClub functionality.

## Table of Contents

- [Installation](#installation)
- [Peer Dependencies](#peer-dependencies)
- [iOS Configuration](#ios-configuration)
- [Usage](#usage)
- [API Reference](#api-reference)

## Installation

1. Create a new file in your root called .npmrc with these lines:
```ini
@statclub:registry=https://registry.npmjs.org/
//registry.npmjs.org/:_authToken=<your_auth_token>
```

2. Install the package:
```bash
npm install @statclub/widget
# or
yarn add @statclub/widget
```

## Peer Dependencies

Install the required peer dependencies (install-deps.sh exists inside of the widget's dist folder):

```terminal
bash install-deps.sh
```

## iOS Configuration

Add the following keys to your `Info.plist` file (if not already present):

```xml
<key>NSLocationAlwaysAndWhenInUseUsageDescription</key>
<string>Statclub uses your location to see which events your have previously attended to power your event map.</string>

<key>NSLocationWhenInUseUsageDescription</key>
<string>Statclub uses your location to see which events your have previously attended to power your event map.</string>

<key>NSPhotoLibraryAddUsageDescription</key>
<string>StatClub needs access to your camera roll to detect the events you've been to and group photos into event albums.</string>

<key>NSPhotoLibraryUsageDescription</key>
<string>StatClub needs access to your camera roll to detect the events you've been to and group photos into event albums.</string>
```

## Usage

### 1. Configure Tailwind CSS

Update your `tailwind.config.js` to include the widget's components in the content scanning path:

```javascript
// tailwind.config.js
module.exports = {
  content: [
    './src/**/*.{js,ts,jsx,tsx}',
    // Add the widget's distribution files
    './node_modules/@statclub/widget/dist/**/*.{js,ts,jsx,tsx}',
  ],
  // ... rest of your config
};
```

### 2. Initialize the Widget Environment

**⚠️ IMPORTANT**: You must initialize the widget environment before rendering the widget component. Call one of these functions in your app's entry point (e.g., `App.tsx` or `index.js`):

#### For Expo Projects
```jsx
import { Widget, initWidgetForExpo } from '@statclub/widget';

// Call this early in your app, before rendering the Widget
initWidgetForExpo();
```

#### For Bare React Native Projects
```jsx
import { Widget, initWidgetForBare } from '@statclub/widget';

// Call this early in your app, before rendering the Widget
initWidgetForBare();
```

**Note**: If you don't call one of these initialization functions, the widget will display an error message asking you to initialize the environment properly.

### 3. Import and Use the Widget

```jsx
import { Widget, initWidgetForExpo } from '@statclub/widget';
// or for bare React Native: import { Widget, initWidgetForBare } from '@statclub/widget';

// Initialize environment early in your app
initWidgetForExpo(); // or initWidgetForBare() for bare React Native

function MyScreen() {
  return (
    <View style={{ flex: 1 }}>
      {/* Your other components */}
      <Widget 
        orgId="test-org-123"
        hostId="test-host-456"
        userId="test-user-789"
        userEmail="test@example.com"
        sportIds={["34690", "34691", "34692"]}
        theme="dark"
      />
    </View>
  );
}
```

## API Reference

### Widget Props

| Prop | Type | Required | Description |
|------|------|----------|-------------|
| `orgId` | `string` | Yes | Organization identifier |
| `hostId` | `string` | Yes | Host identifier |
| `userId` | `string` | Yes | User identifier |
| `userEmail` | `string` | Yes | User's email address |
| `theme` | `'light' \| 'dark'` | No | Theme preference (defaults to 'light') |
| `sportIds` | `string[]` | No | Array of sport IDs to filter events |

## Support

For issues and questions, please contact the package maintainer or refer to the StatClub documentation. 