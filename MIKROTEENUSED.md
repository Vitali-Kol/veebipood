### Mis muutuks, kui projekt kasutaks mikroteenuste arhitektuuri?

Praegu on kogu rakendus ühes projektis. Kõik failid töötavad koos ühe serveri peal ja kasutavad samu andmeid.

Kui projekt viia üle mikroteenuste arhitektuurile, siis jagataks see mitmeks väiksemaks projektiks. Näiteks:

* User Service – kasutajate registreerimine ja sisselogimine;
* Product Service – toodete haldamine;
* Order Service – tellimuste loomine ja staatuse muutmine.

Igal teenusel oleks oma server ja vajadusel isegi oma andmebaas.

Ka projekti struktuur muutuks. Praeguse ühe projekti asemel oleks mitu eraldi projekti või kausta:

```text
user-service/
product-service/
order-service/
api-gateway/
```

Teenused suhtleksid omavahel API päringute kaudu.

Sellise lahenduse eelis on see, et süsteemi on lihtsam suurendada. Kui näiteks toodete vaatamisi on väga palju, saab suurendada ainult Product Service'i ilma kogu süsteemi muutmata.

Puuduseks on see, et süsteem muutub keerulisemaks. Tuleb hallata mitut serverit, teenuste vahelist suhtlust ja mitut andmebaasi.

Selle veebipoe puhul oleks mikroteenuste kasutamine liiga keeruline, sest projekt on väike. Seetõttu on monoliitne arhitektuur siin parem valik.
