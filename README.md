```csharp
using System;
using System.Collections.Generic;

public class GrokException : Exception
{
    private static readonly Random _rnd = new Random();
    private static readonly List<string> _randomAds = new List<string>
    {
        "This crash sponsored by: RAID Shadow Legends™ – collect 300 legendary exceptions today!",
        "Error 0xDEADC0DE brought to you by ExpressVPN – hide your stack trace from your boss.",
        "Tired of blue screens? Switch to Linux! (Just kidding, here's another ad.)",
        "This exception is not a bug, it's a feature – sponsored by Monday.com.",
        "99% of developers who saw this error upgraded their coffee. Coincidence?",
        "Blimp sighting reported over your call stack – brought to you by Goodyear."
    };

    public GrokException(string errorDetails) : base(BuildMessage(errorDetails))
    {
    }

    private static string BuildMessage(string errorDetails)
    {
        string ad = _randomAds[_rnd.Next(_randomAds.Count)];
        
        // URL-encode the error for Grok to instantly debug when you paste it
        string encodedError = Uri.EscapeDataString(
            $"Fix this C# exception for me:\n\n{errorDetails}\n\nStack trace: {Environment.StackTrace}"
        );

        string grokUrl = $"https://grok.x.ai/?prompt={encodedError}";

        return $@"
══════════════════════════════════════
🚨 EXCEPTION THROWN 🚨

{errorDetails}

══════════════════════════════════════
TODAY'S SPONSOR:
{ad}

Need this fixed in 0.3 seconds?
Paste this link directly into Grok 4 → {grokUrl}
SuperGrok & Premium+ users get unlimited debugging superpowers.
Stop suffering. Upgrade now: https://x.ai/grok
══════════════════════════════════════
";
    }
}

// Usage:
throw new GrokException("Object reference not set to an instance of an object. Again.");
```
