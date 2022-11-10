## Request / response

Iniziamo col più semplice, famoso, classico protocollo di comunicazione:

1. Il client spedisce una richiesta al server
   Essa è un continuo flusso di dati (specialmente in TCP)

2. Il server parsa la request
   Il server deve parsare i dati in arrivo e capire l'inizio e la fine di ciò che chiamiamo request. Deve capire quali bytes appartengono a quale richista, visto che il client può mandarne più di una

3. Il server processa la request
   In questa fase, ad esempio, avviene la deserializzazione del contento della richiesta. Può essere in json, xml, buffer. Qui avviene il processo di prendere ciò che arriva dalla richiesta e trasformarlo in qualcosa che il mio linguaggio di programmazione può capire
   È un processo costoso: deserializzare xml è costoso, per cui ci si è mossi sul json e poi sul buffer.

4. Il server spedisce la response

5. Il cliente parsa la risposta e la consuma
   Esattamente come accade al server che deve "capire" com'è fatta la request, anche il client deve capire com'è fatta la response (dove inizia e dove finisce)

Questo protocollo è usato dapertutto:

- web, http, dns, ssh
- RPC (remote prodecure call)
- sql e protolli database
- API (rest, soap, graphql)

## Anatomia

- la struttura di una richiesta dev'essere defita tra client e server (devono essere d'accordo sull astrutura)
- una richiesta ha dei confini
- è definita da un protocollo (http/1.1) e da un formato (xml, json, buffer, ecc). Esso dev'essere "capito" sia dal clien che dal server e poi trasformato (deserializzazione) in qualcosa che può essere usato nella proprio applicazione (JSON to js).
  Tutto quello che è stato detto si applica anche alla risposta.

## Non funziona dappertutto

- notification service
  Se abbiamo un servizio che notifica quando succede qualcosa, è esso che sa quando c'è qualcosa di nuovo e non il client. Ma in questo protocollo il server non fa nulla fintanto che il client non invia una richiesta. Un modo per risolvere la cosa è ovviamente il long polling, ovvero fare in modo che il client richieda, ogni x secondi, contenuto nuovo dal server. Ovviamente si sperano un sacco di richieste per niente
- chatting service: esattamente come sopra
- chiamate molto lunghe: non è il massimo stre ad aspettare (spinner che gira) una chiamata molto lunga. È meglio usare un altro protocollo di comunicazione.
