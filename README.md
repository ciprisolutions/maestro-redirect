

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

        // --- utm_campaign: phone, digits only
        const phoneRaw = params.get("utm_campaign"); // decoded
        if (phoneRaw) {
          const digits = phoneRaw.replace(/\D+/g, "");
          const last11 = digits.slice(-11);
          if (last11.length === 11) {
            params.set("utm_campaign", last11);
          }
        }

        // Build redirect URL
        const outUrl = new URL(DEST);
        outUrl.search = params.toString();

        // Redirect
        window.location.replace(outUrl.toString());
      })();
    </script>

