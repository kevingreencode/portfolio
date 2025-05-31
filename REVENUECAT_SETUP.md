# RevenueCat Setup for Cosmos Holo

This guide will help you set up RevenueCat for subscription management in the Cosmos Holo app.

## 🎯 Pricing Structure

- **7-Day Free Trial** then **Monthly Pro**: $0.99/month 
- **Lifetime Pro**: $9.99 one-time payment
- **No permanent free version** - users must start trial or purchase

## 📋 Prerequisites

1. Apple Developer Account
2. App Store Connect access
3. RevenueCat account (free tier available)

## 🚀 Setup Steps

### 1. Create RevenueCat Account

1. Go to [RevenueCat](https://www.revenuecat.com/)
2. Sign up for a free account
3. Create a new project called "Cosmos Holo"

### 2. Configure App Store Connect

1. In App Store Connect, go to your Cosmos Holo app
2. Navigate to **Features** → **In-App Purchases**
3. Create two products:

#### Monthly Subscription
- **Product ID**: `com.cosmosholo.monthly_premium`
- **Reference Name**: Cosmos Holo Pro Monthly
- **Type**: Auto-Renewable Subscription
- **Subscription Group**: Create new group "Cosmos Holo Pro"
- **Price**: $0.99/month
- **Free Trial**: 7 days

#### Lifetime Purchase
- **Product ID**: `com.cosmosholo.lifetime_premium`
- **Reference Name**: Cosmos Holo Pro Lifetime
- **Type**: Non-Consumable
- **Price**: $9.99

### 3. Configure RevenueCat Dashboard

1. In RevenueCat dashboard, go to **Project Settings**
2. Add your app:
   - **App Name**: Cosmos Holo
   - **Bundle ID**: Your app's bundle identifier
   - **Platform**: iOS
3. Go to **Products** and add:
   - Monthly: `com.cosmosholo.monthly_premium`
   - Lifetime: `com.cosmosholo.lifetime_premium`
4. Create an **Entitlement** called "premium"
5. Attach both products to the "premium" entitlement

### 4. Get API Keys

1. In RevenueCat, go to **API Keys**
2. Copy your **Public SDK Key** for iOS
3. You'll need both sandbox and production keys

### 5. Update App Configuration

1. Open `src/context/SubscriptionContext.tsx`
2. Update the API key configuration:

```typescript
// Replace with your actual API keys
const apiKey = __DEV__ 
  ? 'appl_YOUR_SANDBOX_KEY_HERE' 
  : 'appl_YOUR_PRODUCTION_KEY_HERE';
```

3. Set the testing flag to true:

```typescript
const TEST_WITH_REVENUECAT = true;
```

### 6. Test Subscription Flow

1. Create a sandbox test user in App Store Connect
2. Sign out of App Store on your test device
3. Sign in with sandbox test user
4. Test the subscription flow in your app

## �� Premium Features

All features require either an active trial, subscription, or lifetime access:

- ✅ **Card Analysis** - Professional centering measurement tools
- ✅ **Export Analysis Images** - Download analysis results to photo library
- ✅ **Unlimited Analyses** - No limits on number of card analyses
- ✅ **Advanced Measurements** - Enhanced precision tools
- ✅ **Premium Themes** - Additional app themes and customization
- ✅ **Detailed Reports** - Comprehensive analysis reports
- ✅ **Custom Guidelines** - Personalized measurement guidelines

## 🚀 User Flow

1. **New Users**: Presented with trial welcome screen
2. **Trial Options**: 
   - Start 7-day free trial (then $0.99/month)
   - Purchase lifetime access ($9.99)
3. **Post-Trial**: Must subscribe or purchase to continue
4. **No Free Tier**: App requires active subscription for all features

## 🧪 Development Testing

During development, the app uses AsyncStorage to simulate subscription states:

- Free trial can be started without RevenueCat
- Subscription status is persisted locally
- Premium features can be tested without real purchases

To enable real RevenueCat testing, set `TEST_WITH_REVENUECAT = true` in `SubscriptionContext.tsx`.

## 📱 App Store Review

When submitting to App Store:

1. Ensure subscription terms are clearly displayed
2. Include privacy policy link
3. Test restore purchases functionality
4. Verify subscription management works correctly

## 🔗 Useful Links

- [RevenueCat Documentation](https://docs.revenuecat.com/)
- [App Store Connect Guide](https://developer.apple.com/app-store-connect/)
- [iOS Subscription Best Practices](https://developer.apple.com/app-store/subscriptions/)

## 🆘 Troubleshooting

### Common Issues

1. **Products not loading**: Ensure product IDs match exactly between App Store Connect and RevenueCat
2. **Sandbox testing fails**: Make sure you're signed in with a sandbox test user
3. **Restore purchases not working**: Check that entitlements are properly configured

### Debug Logs

Enable debug logging in development:

```typescript
if (__DEV__) {
  await Purchases.setLogLevel(LOG_LEVEL.DEBUG);
}
```

This will show detailed RevenueCat logs in your console to help debug issues. 