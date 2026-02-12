
<html>
  <head>
    <meta charset="utf-8" />
    <meta name="robots" content="noindex,nofollow" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Redirecting…</title>
  </head>
  <body>

    <script>
      (function () {
        const DEST = "https://buy.stripe.com/3cI7sN2SRfDg4fG1jx8bS03";

        // Parse incoming params
        const inUrl = new URL(window.location.href);
        const params = new URLSearchParams(inUrl.search);

        // --- utm_medium: email with safe replacements
        const emailRaw = params.get("utm_medium"); // decoded automatically
        if (emailRaw) {
          const emailSafe = emailRaw
            .replace("@", "yyyyy")
            .replace(/\./g, "zzzzz"); // replace all dots
          params.set("utm_medium", emailSafe);
        }

        // --- utm_campaign: phone, digits only, last 10
        const phoneRaw = params.get("utm_campaign"); // decoded
        if (phoneRaw) {
          const digits = phoneRaw.replace(/\D+/g, "");
          const last10 = digits.slice(-10);
          if (last10.length === 10) {
            params.set("utm_campaign", last10);
          }
        }

        // Build redirect URL
        const outUrl = new URL(DEST);
        outUrl.search = params.toString();

        // Redirect
        window.location.replace(outUrl.toString());
      })();
    </script>
  </body>
</html>
