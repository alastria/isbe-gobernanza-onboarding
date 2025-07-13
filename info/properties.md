# Comparación de did:elsi con did:isbe

**Madurez**
- 🟩 elsi: En producción en un contexto internacional desde hace más de un año.
- 🟥 isbe: Todavía en diseño, y faltan detalles críticos.

**Posibilidad de firma cualificada o avanzada con certificado cualificado**
- 🟩 elsi: Basado en certificado cualificado emitido por cualquier QTSP Europeo, que permite firma cualificada (certificado cualificado y QSCD) o firma avanzada con certificado cualificado (certificado cualificado sin QSCD).
  
  Aunque eIDAS no requiere certificado cualificado para una firma avanzada, tanto el ENS como muchas aplicaciones sectoriales (por ejemplo banca o salud) requieren un certificado cualificado aunque se use una firma avanzada, cuando el nivel de seguridad requerido es medio o alto.

- 🟥 isbe: El documento de diseño no define el marco específico, politicas y entorno regulatorio en el cual se generan las claves privadas, pero de la documentación que existe se puede deducir que no se pueden conseguir ni firmas cualificadas ni firmas avanzadas con certificado cualificado.
  
  Esto quiere decir que los sectores y aplicaciones que requieren una firma con certificado cualificado no pueden usar Credenciales Verificables basadas en did:isbe. Por ejemplo, la Administración pública (por el ENS).

**Facilidad de adopción por el sector público**
- 🟩 elsi: Para las administraciones públicas que actualmente emiten y reciben documentos firmados electrónicamente, una Credencial Verificable con una firma JAdES usando el did:elsi como identificador único se puede considerar como un documento emitido/recibido en un formato adicional, simplemente con un mecanismo de transmisión diferente (OID4VCI/OID4VP). El identificador único de la organización es exactamente el mismo que usan actualmente (con la única diferencia de un prefijo constante). En emisión se puede usar el mismo certificado que se usa para la firma/sello de los otros documentos, y en recepción el proceso de verificación de firma de la organización o representante y sus consideraciones legales/cumplimiento son muy parecidas.
- 🟥 isbe: Falta información de detalle en como realiza el proceso de firma en did:isbe, pero de la documentación que existe se puede deducir que en emisión el proceso es completamente diferente al que usan actualmente, y además existen muchas dudas sobre el tipo de firma que se puede conseguir (desde luego, nunca puede ser una firma cualificada o una firma con certificado cualificado), ya que el proceso de generación de la clave privada y artefactos asociados no cumple con los requerimientos necesarios para ello.

**Facilidad de adopción por el sector privado**

- 🟩 elsi: Aplican las mismas consideraciones que en el sector público, aunque en entornos B2B se podrían llegar a acuerdos que utilizaran did:isbe, si las entidades privadas están dispuestas a aceptar el riesgo legal y operacional asociado.
  
  No obstante, al menos para entidades privadas en sectores regulados, es dudoso que los responsables de cumplimiento acepten esos riesgos asociados al did:isbe, cuando existe la opcion del did:elsi que tiene casi las mismas implicaciones que los sistemas de firma usados actualmente.

  Además, en cuanto las entidades privadas deban interactuar con la Administración pública, aplican las mismas consideraciones que para la Administración pública.

- 🟥 isbe: Ver la justificación en el punto de did:elsi.

**Generación del identificador**
- 🟩 elsi: Generado por las autoridades competentes en cada pais miembro. El identificador es uno de los identificadores únicos asociados a la organización y de obligado uso por la regulación en su campo de utilización.
- 🟥 isbe: Generado aleatoriamente, y en principio no asociado a la identidad real de la organización.

**Asociación del identificador con la identidad real de la organización**
- 🟩 elsi: Asociado por la entidad regulada correspondiente. Hay una relación 1:1 entre el DID y un identificador único asociado por una entidad regulada a la organización. A partir del DID se puede obtener la identidad real de la organización sin necesidad de una entidad intermedia diferente de las reguladas, y sin consultar a ningún repositorio mantenido por entidades diferentes (como ISBE o su red).
- 🟥 isbe: Asociado por un mecanismo no regulado. En la documentación del método `isbe` todavía no está definido si la asociación será como una declaración responsable o si en ISBE se realizará una validación de la asociación entre el identificador y la identidad real de la organización. En cualquiera de los dos casos, impide realizar firmas cualificadas o incluso avanzadas con certificado cualificado, a menos que ISBE se constituya en un QTSP.

**Interoperabilidad fuera del ecosistema ISBE**
- 🟩 elsi: El identificador tiene relación 1:1 con alguno de los identificadores únicos oficiales de la organización reconocidos a nivel pan-Europeo (incluso global, como el LEI) y además está asociado por un QTSP con material criptográfico que permite demostrar a la organización esa asociación con un nivel alto de confianza. El uso de did:elsi no está ligado a ISBE y se puede usar fuera del ecosistema por organizaciones que no necesitan ni pertenecer a ISBE ni usar APIs u otros mecanismos específicos a ISBE. Incluso en el caso extremo de que ISBE desapareciese, el mecanismo did:elsi por su naturaleza, seguiría funcionando.
- 🟥 isbe: Solo aplicable a ecosistema ISBE, requiere que las organizaciones que lo usen pertenezcan a ISBE o usen APIs de terceros que estén en ISBE. Si ISBE desaparece, el mecanismo deja de funcionar, por su alta dependencia.

**Rol de ISBE y descentralización**
- 🟩 elsi: El mecanismo no depende de ISBE, sino del marco global Europeo eIDAS/eIDAS2 y su infraestructura distribuida, por lo que se consigue la máxima descentralización posible con alto cumplimiento regulatorio. ISBE no tiene ninguna capacidad técnica para modificar la parte core del DID Document, por lo que incluso un compromiso de todo ISBE no afecta a la seguridad del método did:elsi.
- 🟥 isbe: ISBE tiene la capacidad técnica para modificar cualquier DID Document, y debe realizar un ejercicio consciente de voluntad para no asumir un rol centralizado de control. Un compromiso/hackeo de ISBE puede comprometer la seguridad del DID Document asociado (al menos no existe ningún documento que detalle como se pordría evitar este problema con el did:isbe).

**Robustez y resiliencia**
- 🟩 elsi: Alta, esecnialmente la misma robustez y resiliencia que los mecanismos actuales de firma electrónica en la UE, existentes desde hace una década. No hay ninguna entidad nueva que requiera infraestructura nueva y no probada.
- 🟥 isbe: Desconocida, por no existir ninguna implementación en producción todavía. Pero de la documentación existente se deduce que la dependencia de ISBE es muy alta, por lo que su robustez y resiliencia es mucho menor que para did:elsi.

**Multiplicidad de identificadores para una misma organización**
- 🟩 elsi: Una organización puede tener diferentes identificadores únicos, pero deben ser alguno de los identificadores únicos oficiales que deben ser usados obligatoriamente en los ámbitos correspondientes. Por ejemplo, en la relación con la Administración pública española, una empresa se debe identificar con el NIF, tanto para la contratación, facturación, notificaciones, etc. Cualquier Credencial Verificable que sea usada en este ámbito debe usar como identificador único el NIF, nunca otro identificador no reconocido "inventado".
- 🟥 isbe: Se basa en potencialmente múltiples identificadores únicos no reconocidos y que no se pueden usar en la mayoría de los casos en que una empresa intercambia Credenciales Verificables con otras empresas, ciudadanos o la Administración pública española.






<style>
   .tablecentered th {
      text-align: center;
   }
</style>


<table class="tablecentered">

<thead>
<tr>
<th>

**did:elsi**

</th>
<th>

**did:isbe**

</th>
</tr>
</thead>

<tbody>

<tr>
<th colspan="2">

**Robustez y resiliencia**

</th>
</tr>

<tr>
<td>

🟩 elsi: Alta, esencialmente la misma robustez y resiliencia que los mecanismos actuales de firma electrónica en la UE, existentes desde hace una década. No hay ninguna entidad nueva que requiera infraestructura nueva y no probada.

</td>
<td>

🟥 isbe: Desconocida, por no existir ninguna implementación en producción todavía. Pero de la documentación existente se deduce que la dependencia de ISBE es muy alta, por lo que su robustez y resiliencia es mucho menor que para did:elsi.

</td>
</tr>


<tr>
<th colspan="2">

**Madurez**

</th>
</tr>

<tr>
<td>

🟩 elsi: En producción en un contexto internacional desde hace más de un año.

</td>
<td>

🟥 isbe: Todavía en diseño, y faltan detalles críticos.

</td>
</tr>


<tr>
<th colspan="2">

**Posibilidad de firma cualificada o avanzada con certificado cualificado**

</th>
</tr>

<tr>
<td>

🟩 elsi: Basado en certificado cualificado emitido por cualquier QTSP Europeo, que permite firma cualificada (certificado cualificado y QSCD) o firma avanzada con certificado cualificado (certificado cualificado sin QSCD).
  
Aunque eIDAS no requiere certificado cualificado para una firma avanzada, tanto el ENS como muchas aplicaciones sectoriales (por ejemplo banca o salud) requieren un certificado cualificado aunque se use una firma avanzada, cuando el nivel de seguridad requerido es medio o alto.

</td>
<td>

🟥 isbe: El documento de diseño no define el marco específico, politicas y entorno regulatorio en el cual se generan las claves privadas, pero de la documentación que existe se puede deducir que no se pueden conseguir ni firmas cualificadas ni firmas avanzadas con certificado cualificado.
  
Esto quiere decir que los sectores y aplicaciones que requieren una firma con certificado cualificado no pueden usar Credenciales Verificables basadas en did:isbe. Por ejemplo, la Administración pública (por el ENS).

</td>
</tr>


<tr>
<th colspan="2">

**Facilidad de adopción por el sector público**

</th>
</tr>

<tr>
<td>

🟩 elsi: Para las administraciones públicas que actualmente emiten y reciben documentos firmados electrónicamente, una Credencial Verificable con una firma JAdES usando el did:elsi como identificador único se puede considerar como un documento emitido/recibido en un formato adicional, simplemente con un mecanismo de transmisión diferente (OID4VCI/OID4VP). El identificador único de la organización es exactamente el mismo que usan actualmente (con la única diferencia de un prefijo constante). En emisión se puede usar el mismo certificado que se usa para la firma/sello de los otros documentos, y en recepción el proceso de verificación de firma de la organización o representante y sus consideraciones legales/cumplimiento son muy parecidas.

</td>
<td>

🟥 isbe: Falta información de detalle en como realiza el proceso de firma en did:isbe, pero de la documentación que existe se puede deducir que en emisión el proceso es completamente diferente al que usan actualmente, y además existen muchas dudas sobre el tipo de firma que se puede conseguir (desde luego, nunca puede ser una firma cualificada o una firma con certificado cualificado), ya que el proceso de generación de la clave privada y artefactos asociados no cumple con los requerimientos necesarios para ello.

</td>
</tr>


<tr>
<th colspan="2">

**Facilidad de adopción por el sector privado**

</th>
</tr>

<tr>
<td>

🟩 elsi: Aplican las mismas consideraciones que en el sector público, aunque en entornos B2B se podrían llegar a acuerdos que utilizaran did:isbe, si las entidades privadas están dispuestas a aceptar el riesgo legal y operacional asociado.
  
No obstante, al menos para entidades privadas en sectores regulados, es dudoso que los responsables de cumplimiento acepten esos riesgos asociados al did:isbe, cuando existe la opcion del did:elsi que tiene casi las mismas implicaciones que los sistemas de firma usados actualmente.

Además, en cuanto las entidades privadas deban interactuar con la Administración pública, aplican las mismas consideraciones que para la Administración pública.

</td>
<td>

🟥 isbe: Ver la justificación en el punto de did:elsi.

</td>
</tr>


<tr>
<th colspan="2">

**Generación del identificador**

</th>
</tr>

<tr>
<td>

🟩 elsi: Generado por las autoridades competentes en cada pais miembro. El identificador es uno de los identificadores únicos asociados a la organización y de obligado uso por la regulación en su campo de utilización.

</td>
<td>

🟥 isbe: Generado aleatoriamente, y en principio no asociado a la identidad real de la organización.

</td>
</tr>


<tr>
<th colspan="2">

**Asociación del identificador con la identidad real de la organización**

</th>
</tr>

<tr>
<td>

🟩 elsi: Asociado por la entidad regulada correspondiente. Hay una relación 1:1 entre el DID y un identificador único asociado por una entidad regulada a la organización. A partir del DID se puede obtener la identidad real de la organización sin necesidad de una entidad intermedia diferente de las reguladas, y sin consultar a ningún repositorio mantenido por entidades diferentes (como ISBE o su red).

</td>
<td>

🟥 isbe: Asociado por un mecanismo no regulado. En la documentación del método `isbe` todavía no está definido si la asociación será como una declaración responsable o si en ISBE se realizará una validación de la asociación entre el identificador y la identidad real de la organización. En cualquiera de los dos casos, impide realizar firmas cualificadas o incluso avanzadas con certificado cualificado, a menos que ISBE se constituya en un QTSP.

</td>
</tr>


<tr>
<th colspan="2">

**Interoperabilidad fuera del ecosistema ISBE**

</th>
</tr>

<tr>
<td>

🟩 elsi: El identificador tiene relación 1:1 con alguno de los identificadores únicos oficiales de la organización reconocidos a nivel pan-Europeo (incluso global, como el LEI) y además está asociado por un QTSP con material criptográfico que permite demostrar a la organización esa asociación con un nivel alto de confianza. El uso de did:elsi no está ligado a ISBE y se puede usar fuera del ecosistema por organizaciones que no necesitan ni pertenecer a ISBE ni usar APIs u otros mecanismos específicos a ISBE. Incluso en el caso extremo de que ISBE desapareciese, el mecanismo did:elsi por su naturaleza, seguiría funcionando.

</td>
<td>

🟥 isbe: Solo aplicable a ecosistema ISBE, requiere que las organizaciones que lo usen pertenezcan a ISBE o usen APIs de terceros que estén en ISBE. Si ISBE desaparece, el mecanismo deja de funcionar, por su alta dependencia.

</td>
</tr>


<tr>
<th colspan="2">

**Rol de ISBE y descentralización**

</th>
</tr>

<tr>
<td>

🟩 elsi: El mecanismo no depende de ISBE, sino del marco global Europeo eIDAS/eIDAS2 y su infraestructura distribuida, por lo que se consigue la máxima descentralización posible con alto cumplimiento regulatorio. ISBE no tiene ninguna capacidad técnica para modificar la parte core del DID Document, por lo que incluso un compromiso de todo ISBE no afecta a la seguridad del método did:elsi.

</td>
<td>

🟥 isbe: ISBE tiene la capacidad técnica para modificar cualquier DID Document, y debe realizar un ejercicio consciente de voluntad para no asumir un rol centralizado de control. Un compromiso/hackeo de ISBE puede comprometer la seguridad del DID Document asociado (al menos no existe ningún documento que detalle como se pordría evitar este problema con el did:isbe).

</td>
</tr>


<tr>
<th colspan="2">

**Robustez y resiliencia**

</th>
</tr>

<tr>
<td>

🟩 elsi: Alta, esecnialmente la misma robustez y resiliencia que los mecanismos actuales de firma electrónica en la UE, existentes desde hace una década. No hay ninguna entidad nueva que requiera infraestructura nueva y no probada.

</td>
<td>

🟥 isbe: Desconocida, por no existir ninguna implementación en producción todavía. Pero de la documentación existente se deduce que la dependencia de ISBE es muy alta, por lo que su robustez y resiliencia es mucho menor que para did:elsi.

</td>
</tr>


<tr>
<th colspan="2">

**Multiplicidad de identificadores para una misma organización**

</th>
</tr>

<tr>
<td>

🟩 elsi: Una organización puede tener diferentes identificadores únicos, pero deben ser alguno de los identificadores únicos oficiales que deben ser usados obligatoriamente en los ámbitos correspondientes. Por ejemplo, en la relación con la Administración pública española, una empresa se debe identificar con el NIF, tanto para la contratación, facturación, notificaciones, etc. Cualquier Credencial Verificable que sea usada en este ámbito debe usar como identificador único el NIF, nunca otro identificador no reconocido "inventado".

</td>
<td>

🟥 isbe: Se basa en potencialmente múltiples identificadores únicos no reconocidos y que no se pueden usar en la mayoría de los casos en que una empresa intercambia Credenciales Verificables con otras empresas, ciudadanos o la Administración pública española.

</td>
</tr>

</tbody>
</table>



