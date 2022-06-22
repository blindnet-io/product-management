# devkit Data Model

This document specifies blindnet devkit data model. It is based on the [Privacy Request Interchange Vocabulary][priv]. More details about each of the concepts and properties can be found in [PRIV][priv].

All components of the devkit, when dealing with concepts described in this model, must follow the model.

Figure below specifies the model around [Privacy Request][prreq].
<img src="./img/devkit_privacy_request.png">
<br><br>

Figure below specifies the model around [Privacy Request Response][prreqresp].
<img src="./img/devkit_priv_req_response.png">
<br><br>

Figure below specifies the model around [Data Capture][dc] and [Data Fragments][df].
<img src="./img/devkit_capture.png">
<br><br>

Figure below specifies the model around [Consents][consent].
<img src="./img/devkit_consent.png">
<br><br>

[priv]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md
[prreq]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#privacy-request
[prreqresp]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#privacy-request-response
[dc]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#data-capture
[df]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#data-capture-fragments
[consent]: https://github.com/blindnet-io/product-management/blob/devkit-schemas/refs/schemas/priv/RFC-PRIV.md#consent
