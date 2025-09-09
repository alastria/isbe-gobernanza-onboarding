# ISBE-ARTIFACT-04010 - Onboarding de empresas a ISBE

## **1. Identificación del Artefacto**

| Campo                     | Valor                                                                                                                                                                                                                       |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Nombre del artefacto**  | ISBE-ART-04010 — Onboarding de empresas a ISBE                                                                                                                                                                              |
| **Origen**                | Conjunto de soluciones que permiten a las empresas poseedoras de un certificado digital realizar el onboarding a la plataforma ISBE de manera self-service y obtener una credencial verificable como resultado del proceso. |
| **Estado**                | *En desarrollo*                                                                                                                                                                                                             |
| **Versión del documento** | *0.1.0*                                                                                                                                                                                                                     |
| **Fecha**                 | *2025-09-09*                                                                                                                                                                                                                |
| **Repositorio**           | [https://github.com/alastria/isbe-gobernanza-onboarding](https://github.com/alastria/isbe-gobernanza-onboarding)                                                                                                            |
| **Commit**                | N/A                                                                                                                                                                                                                         |

## **2. Propósito del Artefacto**

- **Objetivo funcional:** Facilitar el registro y acceso de empresas en ISBE mediante un flujo de alta 100% digital, utilizando certificados digitales cualificados. El sistema valida el certificado presentado, permite completar un formulario de datos básicos y emite una credencial verificable.

- **Beneficio para ISBE:** Asegura un onboarding ágil, estandarizado y conforme a normativa para empresas, reduciendo costes de verificación manual y garantizando interoperabilidad con el ecosistema europeo (EBSI).

- **Stakeholders clave:**  
  - **Equipos técnicos ISBE**: desarrollo, despliegue e integración de los componentes de Onboarding, Issuer y Verifier. 
  - **Empresas usuarias**: identificación simplificada y acceso a los servicios y red ISBE. 
  - **Reguladores y auditores**: cumplimiento de normativa eIDAS2, GDPR. 
  - **Otros proveedores**: integraciones con Trust Anchor y Wallet externos.

## **3. Alcance y Ciclo de Vida**

- **Fases cubiertas:**

  - 🟡 **Planificación:** acotar alcance, dependencias externas (Trust Anchor ISBE/EBSI, Wallets), y plan de entregas (MVP y evolutivos). [Plan de proyecto](../proyecto/PLAN_DE_PROYECTO.md) 
  
  - 🟡 **Análisis:** convertir el alcance en requisitos verificables y contratos funcionales. [Documento Técnico](../proyecto/DOCUMENTO_TECNICO.md)
  
  - 🟡 **Diseño:** diseñar componentes, interfaces y seguridad end-to-end. [Documento de Diseño](../proyecto/DOCUMENTO_DISE%C3%91O.md) 
  
  - 🟡 **Implementación:** construir y configurar los componentes comprometidos.
  
  - 🟡 **Pruebas:** asegurar conformidad funcional, interoperabilidad y NFRs. [Plan de pruebas](../proyecto/PLAN_DE_PRUEBAS.md)
  
  - 🟡 **Despliegue:** poner el servicio en STG y PRD de forma segura y replicable. [Plan de despliegue](../proyecto/PLAN_DE_DESPLIEGUE.md)
  
  - 🟡 **Mantenimiento:** asegurar continuidad operativa, cumplimiento y evolución. [Plan de mantenimiento](../proyecto/PLAN_DE_MANTENIMIENTO.md)
  
  > NOTA: El artefacto cubre el ciclo completo siguiendo la metodología SDLC adaptada a ISBE.

- **Dependencias**:

  - Trust Anchor (externo, operado por otros proveedores) - Red EBSI o ISBE (por definir). 
  
  - Wallet (externo, operado por terceros).
  - Servicio de firma remoto (Digitel TS).
  
  > NOTA: El artefacto no incluye la provisión ni gestión de estos componentes externos, pero depende de su disponibilidad y conformidad.
  
- **Mantenimiento:**

  - Actualización periódica de librerías de validación de certificados.
  
  - Evolución del Issuer/Verifier en función de nuevas releases de protocolos OIDC4VCI / OID4VP. 
  
  - Soporte a nuevas versiones de credenciales verificables y estándares europeos.
  
  > NOTA: El mantenimiento del artefacto se realizará conforme al [Plan de Mantenimiento](../proyecto/PLAN_DE_MANTENIMIENTO.md).

## **4. Definición del Artefacto**

- **4.1. Artefacto de arquitectura de referencia:**

El artefacto **ISBE-ARTIFACT-04010** se fundamenta en una arquitectura de referencia de identidad digital distribuida, en la que el proceso de onboarding de empresas se articula en torno a tres componentes principales provistos por nuestro equipo: **Onboarding Service**, **Issuer Service** y **Verifier Service**.

El diagrama de nivel 2 (C4) representa la interacción entre dichos componentes, los participantes externos y las infraestructuras de confianza:

- **ISBE Participant (Empresa)**: el actor que inicia el proceso presentando su certificado digital cualificado y completando el e-form de registro. 
- **Onboarding Service**: gestiona el flujo de alta, valida la información proporcionada y orquesta las interacciones con el Issuer y el Verifier.
- **Issuer Service**: emite la credencial verificable (**LEARCredentialEmployee**) del LEAR de la empresa registrada en ISBE tras la validación exitosa del certificado y los datos. También registra al nuevo participante en la red de confianza (Trust Anchor). 
- **Verifier Service**: valida certificados digitales y credenciales verificables, asegurando que las empresas y servicios que acceden o participan del ecosistema lo hacen con atributos auténticos y vigentes.
- **Wallet *(externo)***: aplicación en la que el usuario recibe, almacena y gestiona la credencial emitida. Este componente no es provisto por nuestro equipo, pero es esencial para la custodia y el uso posterior de la credencial.
- **Trust Anchor (EBSI/ISBE/LOTL)**: infraestructura externa que mantiene las listas de confianza y entidades válidas. El Issuer y el Verifier dependen de este servicio para realizar la validación y el registro de nuevos participantes.

La arquitectura refleja el paradigma descentralizado de identidad digital:
- El Trust Anchor actúa como fuente de confianza común. 
- El Issuer otorga credenciales verificables tras el onboarding. 
- El Verifier garantiza la validez de los atributos presentados en procesos M2M. 
- El Wallet asegura la soberanía del participante sobre sus credenciales. 

> NOTA: Esta arquitectura permite cumplir con los principios de interoperabilidad (**OID4VCI** y **OID4VP**), alineamiento con **eIDAS2** y resiliencia en un contexto federado, donde cada componente puede evolucionar o ser operado por diferentes entidades sin comprometer el flujo global.

Diagrama C4-Level 2:
```mermaid
C4Context
    title Onboarding de empresas a ISBE - C4-Level 2

    Enterprise_Boundary(b0, "Onboarding System") {
      
      Person(customerA, "ISBE Participant", "Empresa que desea unirse a la red ISBE")
      
      System(SystemE, "Wallet", "Aplicación donde el usuario almacena sus credenciales verificables")
  
      Enterprise_Boundary(b1, "") {
        
        System(SystemB, "Issuer Service", "Servicio que emite credenciales verificables tras el onboarding")
        
        System(SystemC, "Verifier Service", "Servicio que verifica las credenciales y gestiona la validación del certificado digital")
      }
  
      Enterprise_Boundary(b2, "External Systems") {
        
        System(SystemD, "Trust Anchor", "Infraestructura de EBSI o ISBE que contiene las listas de confianza")
      }
  
    }
  
    UpdateElementStyle(customerA, $fontColor="white", $bgColor="#828282", $borderColor="#828282")
    UpdateElementStyle(SystemA, $fontColor="white", $bgColor="#10739E", $borderColor="#10739E")
    UpdateElementStyle(SystemB, $fontColor="white", $bgColor="#10739E", $borderColor="#10739E")
    UpdateElementStyle(SystemC, $fontColor="white", $bgColor="#10739E", $borderColor="#10739E")
    UpdateElementStyle(SystemE, $fontColor="white", $bgColor="#F2931E", $borderColor="#F2931E")
    UpdateElementStyle(SystemD, $fontColor="white", $bgColor="#F2931E", $borderColor="#F2931E")
```

    BiRel(SystemB, SystemC, "Autenticación y autorización con VC de servicio")
    Rel(SystemC, SystemD, "Consulta listas de confianza")
    Rel(SystemA, SystemB, "Solicita emisión de credencial verificable")
    Rel(SystemB, customerA, "Notifica emisión de credencial")
    Rel(customerA, SystemE, "Accede y controla sus credenciales")
    BiRel(SystemB, SystemE, "Entrega credencial verificable")
    Rel(SystemB, SystemD, "Registra participante en la Trust Anchor")


- **4.2. Trazabilidad:**

    Con la arquitectura de referencia:
    - Onboarding Service → responde a los requisitos de acceso self-service de empresas y actúa como orquestador del flujo de registro. 
    - Verifier Service → cubre los requisitos de validación de certificados digitales cualificados y de verificación de credenciales verificables en procesos de autorización posteriores. 
    - Issuer Service → se vincula con los requisitos de emisión de credenciales verificables de empresa registrada, asegurando su conformidad con estándares OID4VCI. 
    - Trust Anchor (externo) → garantiza el cumplimiento de los requisitos de uso de listas de confianza EBSI/ISBE en validaciones. 
    - Wallet (externo) → materializa el principio de soberanía del participante sobre su identidad digital, permitiendo almacenar y presentar las credenciales emitidas. 
    - Service Catalog → demuestra la aplicabilidad de las credenciales emitidas y validadas en un caso de uso real de consumo de servicios ISBE.
  
    Con requisitos funcionales (ejemplos):
    - **ISBE-REQ-0100**: Validación de certificado digital cualificado → Verifier Service + Trust Anchor. 
    - **ISBE-REQ-0110**: Registro de empresa mediante formulario electrónico → Onboarding Service. 
    - **ISBE-REQ-0120**: Emisión de credencial verificable de empresa → Issuer Service. 
    - **ISBE-REQ-0130**: Custodia y presentación de credenciales → Wallet (no provisto por este artefacto). 
    - **ISBE-REQ-0140**: Acceso a servicios del catálogo mediante credenciales verificables → Verifier Service + Service Catalog.
  
    Con requisitos no funcionales (ejemplos):
    - **Seguridad**: validación criptográfica de certificados y credenciales, conforme a eIDAS2 y OIDF. 
    - **Interoperabilidad**: alineamiento con OIDC4VCI (emisión) y OID4VP (presentación). 
    - **Privacidad**: cumplimiento de GDPR mediante minimización de datos y control por parte del participante. 
    - **Disponibilidad y rendimiento**: capacidad de validar certificados en <2s y garantizar 99,5% de uptime en servicios críticos.


- **4.3. Descripción funcional detallada:**

    El artefacto implementa un conjunto de flujos de datos y casos de uso que permiten a una empresa integrarse en la red ISBE, obtener una credencial verificable de registro y utilizarla para acceder a los servicios del ecosistema.

    **Flujos de datos principales**

    1. **Inicio de Onboarding**
       - El participante empresarial accede al Onboarding Service. 
       - Se presenta un certificado digital cualificado (eIDAS QTSP). 
       - El sistema recolecta datos básicos a través de un e-form.
    2. **Validación de identidad**
       - El Verifier Service valida la firma del certificado digital y comprueba su vigencia contra las listas de confianza del Trust Anchor (ISBE/EBSI). 
       - Se aplican reglas de negocio de elegibilidad (certificado activo, no revocado, emitido por QTSP reconocido).
    3. **Emisión de credencial verificable**
       - Una vez validada la identidad, el Issuer Service genera una credencial verificable de empresa registrada en ISBE. 
       - La credencial se entrega al Wallet de la empresa para su custodia.
    4. **Registro en la red de confianza**
       - El Issuer Service comunica al Trust Anchor el alta de la nueva empresa como participante válido de ISBE.
    5. **Uso de credenciales**
       - La empresa utiliza su Wallet para presentar la credencial verificable en procesos de acceso al Service Catalog.
       - El Service Catalog delega en el Verifier Service la validación de la credencial, confirmando la autenticidad y vigencia de la empresa participante.
  
    **Casos de uso cubiertos**

    - **CU-01**. Onboarding self-service de empresa: Alta autónoma en ISBE mediante certificado digital. 
    - **CU-02**. Validación de certificado cualificado: Comprobación criptográfica + listas de confianza. 
    - **CU-03**. Emisión de credencial verificable de empresa: Generación conforme a OIDC4VCI. 
    - **CU-04**. Custodia de credenciales: Delegado a Wallet externo gestionado por la empresa. 
    - **CU-05**. Presentación de credenciales: Uso de OID4VP en el acceso al catálogo de servicios. 
    - **CU-06**. Registro en red de confianza: Alta del participante en Trust Anchor ISBE/EBSI.
    
    **Escenarios cubiertos**

    - **Escenario A**: Onboarding exitoso 
      - El certificado es válido y se emite la credencial. 
      - La empresa queda registrada en la red ISBE.
    - **Escenario B**: Certificado inválido o revocado 
      - El Verifier rechaza la validación. 
      - No se emite credencial, se notifica al usuario.
    - **Escenario C**: Acceso a servicios ISBE
      - La empresa presenta la credencial en el catálogo de servicios. 
      - El Verifier confirma validez y el catálogo otorga acceso.
    - **Escenario D**: Renovación / actualización de credencial
      - En caso de cambio o caducidad del certificado digital, el flujo de onboarding se reinicia para emitir una nueva credencial.

- **4.4. Modelos o diagramas específicos:**

    Diagrama de componentes, interfaces, secuencias, flujos.

  ```mermaid
      sequenceDiagram
  
        participant P as Customer
        participant W as Wallet (tercero)
        
        participant A as Onboarding Service
        participant I as Issuer Service
        
        participant T as Trust Anchor (ISBE/EBSI)
        
        P ->>A: e-form + Cert. cualificado
        A -->>V: |Validación cert.| V
        V -->T: |Listas de confianza / OCSP/CRL| T
        A -->I: |Solicitud emisión| I
        I -->T: |Registro participante| T
        I -->W: |Credential Offer / VC| W
        W -->W: |Almacena VC| W
        S -->V: |AuthZ & VP request| V
        W -->V: |vp_token + presentation_submission| V
        V -->T: |Validación emisor/estado| T
        V -->S: |Tokens/Resultado verificación| S
  ```

- **4.5. Reglas de negocio asociadas:**

    Validaciones, restricciones operativas.

- **4.6. Interfaces y puntos de integración:**

    APIs, endpoints, eventos, contratos de datos.

    Interfaces públicas

- **4.7. Normativas y requisitos regulatorios:**

    RGPD, estándares específicos si aplican.

- **4.8. Criterios de calidad específicos:**

    Rendimiento esperado, seguridad, usabilidad.

## **5. Desarrollo del Artefacto**

- **5.1. Componentes del artefacto:**

    Lista de elementos clave producidos: código, scripts, configuraciones, manuales.

- **5.2. Lista de elementos clave producidos: código, scripts, configuraciones, manuales:**

    Ejemplo: Código, contenedor, JSON, Word, Excel.
    | Nombre | Descripción | Enlace |
    |--------|-------------|--------|
    | Código | Repositorio GitHub | ... |
    | Manual | ... | ... |
    | Última versión liberada | Versiones liberadas y etiquetado de release | ... |

- **5.3. Frameworks, librerías o tecnologías acordadas:**

    Bases técnicas y stack definido.

- **5.4. Buenas prácticas aplicables:**

    Seguridad, rendimiento, mantenibilidad.

- **5.5. Criterios de validación del desarrollo:**

    Pruebas unitarias realizadas, auditorías, evidencias de funcionamiento.

- **5.6. Alineación con requisitos legales (GDPR, NIS2, etc.)**
    si aplica.
- **5.7. Dependencias técnicas o de infraestructura:**

    Sistemas, entornos, herramientas necesarias.

- **5.8. Limitaciones temporales:**

    MVP, iteraciones parciales, restricciones conocidas.

- **5.9. Limitaciones por versiones, licencias o configuraciones.**

## **6. Reglas de Control y Actualización**

- Política de gestión de versiones para la fase de definición y desarrollo.
- Indicar si es actualizable tras la entrega, por quién y bajo qué condiciones.
- Frecuencia de revisión o actualizaciones planificadas.
- Herramienta de control de cambios: repositorio, SharePoint, wiki técnica, etc.

| Tipo de cambio | Versionado | Flujo de aprobación | Documentación requerida |
|---------------|------------|---------------------|------------------------|
| Evolutivo menor | X.Y+0.1 | Pull Request + revisión GT | Release notes detalladas |
| Evolutivo mayor | X+1.0 | Al Comité de ¿?| Impacto |
