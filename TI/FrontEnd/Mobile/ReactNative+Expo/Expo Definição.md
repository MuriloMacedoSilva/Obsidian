
O Expo é um framework e um ecossistema completo para desenvolvimento de aplicações usando React Native.

Enquanto o React Native puro fornece apenas a base (os componentes fundamentais que conectam JavaScript ao código nativo do Android e IOS), o Expo entra como uma camada que abstrrai toda a complexidade de configuração e compilação nativa.

Conceito Principal

A ideia central do Expo é permitir o desenvolvimento de aplicativos nativos sem a necessidade de instalar ferramentas pesadas como Xcode (IOS) ou Android Studio (Android) para começar.


|**Característica**|**React Native "Puro" (CLI)**|**React Native com Expo**|
|---|---|---|
|**Configuração inicial**|Exige ambiente nativo (Android Studio / Xcode)|Apenas Node.js|
|**Pastas Nativas (`/android`, `/ios`)**|Gerenciadas manualmente|Geradas automaticamente (_Continuous Native Generation_)|
|**Testes no dispositivo**|Requer emuladores ou compilação local|Teste direto via aplicativo **Expo Go** no celular|
|**Recursos Nativos**|Requer instalação/configuração manual de bibliotecas|Vem com a **Expo SDK** (câmera, notificações, biometria, GPS, etc.)|

Pilares do Expo : 

**Expo SDK:** Conjunto pronto de bibliotecas nativas e APIs otimizadas para acessar a câmera, sensores, notificações e sistema de arquivos.

**Expo Router:** Sistema de navegação baseado em arquivos (semelhante ao Next.js na web).

**Expo Go:** Aplicativo para dispositivos móveis que lÇe seu código em tempo real via QR Code durante o desenvolvimento, sem precisar compilar.

**EAS (Expo Application Services):** Serviões em nuvem para criar as builds finais (arquivos .apk e .ipa) e enviar a aplicação diretamente para a Google Play e App Store.