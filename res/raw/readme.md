# Introduction

**Aegis** can effectively limit Apps’ behavior using the new device power management API introduced in Android 9 (API level 28). By setting Apps’ the standby mode group, you can easily restrict the Apps’ access to device resources such as CPU or battery, help to ensure that system resources are given to the apps that need them the most.

## Working principle

On Android 9, the system dynamically categorizes each app into a standby group based on the app's time and frequency of use recently. For example, when you open an app, this app will be categorized into the "Active" group immediately. If you haven't used this app for a long time, it will be categorized into the "Rare" group automatically.

During the interval when you are not using the app, it would stay in a higher priority group rather than "Rare" group. As a result, this app will cost more device resources such as CPU or battery. (Those “unruly” apps tend to keep themselves in a higher priority group for a long time unscrupulously.) **Aegis** will break this interval. When your device enters the standby mode, **Aegis** immediately reclassifies the apps to the group previously set by the user, and even force those low-frequency used apps to enter standby mode, thus limiting the Apps’ behavior and improving the battery life of your device.

**Aegis** is the enhanced edition of "Settings - Developer Options - Standby Application", the latter setting is only valid once, when the apps change the group in the way mentioned above, the user's settings won’t work any more, while the effect of **Aegis** is permanent.

## App Standby Buckets

**Active**

> An app is in the active bucket if the user is currently using the app.
>
> If an app is in the active bucket, the system does not place any restrictions on the app's jobs, alarms, or FCM messages.

**Working set**

> An app is in the working set bucket if it runs often but it is not currently active. For example, a social media app that the user launches most days is likely to be in the working set. Apps are also promoted to the working set bucket if they're used indirectly.
>
> If an app is in the working set, the system imposes mild restrictions on its ability to run jobs and trigger alarms.

**Frequent**

> An app is in the frequent bucket if it is used regularly, but not necessarily every day. For example, a workout-tracking app that the user runs at the gym might be in the frequent bucket.
>
> If an app is in the frequent bucket, the system imposes stronger restrictions on its ability to run jobs and trigger alarms, and also imposes a cap on high-priority FCM messages.

**Rare**

> An app is in the rare bucket if it is not often used. For example, a hotel app that the user only runs while they're staying at that hotel might be in the rare bucket.
>
> If an app is in the rare bucket, the system imposes strict restrictions on its ability to run jobs, trigger alarms, and receive high-priority FCM messages. The system also limits the app's ability to connect to the internet.

**Never**

> Apps that have been installed but never run are assigned to the never bucket. The system imposes severe restrictions on these apps.