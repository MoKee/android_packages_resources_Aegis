## Mechanism

On Android 9.0, the system dynamically categorizes each App into a standby group based on the App's recent usage (time and frequency). For example, when an App is opened, it will be categorized into the "Active" group immediately. If users don't open the App for a long time, it will be categorized into the "Rare" group automatically.

During the interval when users are not using the App, some Apps may still stay in a higher priority group instead of the "Rare" group. As a result, this App will still be allocated more resources such as CPU or battery usage (those ill-designed Apps tend to keep themselves in a higher priority group for a long time without user's permission). 

And that's where **Aegis** comes into effect. When your device starts to stand by, **Aegis** will immediately re-categorize these Apps to the corresponding usage group previously set by users, and also force those less-frequently used Apps to start stand by, thus restricting Apps’ behavior and improving the battery life of your device.

# Instructions

* Users can set customized standby groups and policies for different Apps according to habits and usage individually.

  Assuming that you set the App *Amazon* as level "Rare", with the policy being "Standby, and then force stop". The next time you open the App, Android system will temporarily categorize it as "Active". When you stop using that App, and the device start to idle, **Aegis** will automatically re-categorize it into "Rare" group, and kill its background services.  

* By enabling "Disable Chain Wakeup", Apps in usage-restricted groups will be prevented from getting waken up by third party Apps.

* Apps in group "Frequent" and "Rare" will be allowed to start background process only when users start them actively.

* Foreground Apps will be ignored by standby policies. For example, if you leave the screen off while you are gaming (AFK) and causing the device to stand by, no extra standby policies will be applied to the process (which means it will be handled by Android system).

## App Standby Buckets

**Active**

> This group contains Apps which are currently foreground (are currently used by user).
>
> If an App is in the active bucket, the system does not place any restrictions on the App's jobs, alarms, or FCM messages.

**Working set**

> An App is in the Working set bucket if it runs often but it is not currently active. For example, a social media App that the user launches most days is likely to be in the working set. Apps are also promoted to the working set bucket if they're used indirectly.
>
> If an App is in the working set, the system imposes mild restrictions on its ability to run jobs and trigger alarms.

**Frequent**

> An App is in the frequent bucket if it is used regularly, but not necessarily every day. For example, a workout-tracking App that the user runs at the gym might be in the frequent bucket.
>
> If an App is in the frequent bucket, the system imposes stronger restrictions on its ability to run jobs and trigger alarms, and also imposes a cap on high-priority FCM messages.

**Rare**

> An App is in the rare bucket if it is not often used. For example, a hotel App that the user only runs while they're staying at that hotel might be in the rare bucket.
>
> If an App is in the rare bucket, the system imposes strict restrictions on its ability to run jobs, trigger alarms, and receive high-priority FCM messages. The system also limits the App's ability to connect to the Internet.

**Dynamic allocation**

> Android system will dynamically categorize Apps into proper App Standby Buckets according to recent usage (time and frequency). For example, Apps developed by **Google** are trusted in most cases, and these Apps won't abuse system resources, thus they can be set as "Dynamic allocation".
>
> Note that if a App is set as "Dynamic allocation", its activities are handled by Android system, which means **Aegis** will not set restriction on these Apps and will leave them system management.