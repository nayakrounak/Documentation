# CBEFF XML

## CBEFF

* Standards:
  * ISO 19785-3
  * [OASIS patron format ISO/IEC JTC 1 SC 37 - biometrics](https://www.ibia.org/cbeff/iso/bir-header-identifiers), patron identifier 257, patron format identifier 11
  * [OASIS Binary Data Block Format Identifiers](https://www.ibia.org/cbeff/iso/bdb-format-identifiers) for Format Type ISO/IEC JTC 1 SC 37-biometrics, patron identifier 257, BDB patron format identifier 7 for finger image, 8 for face image and 9 for iris image.
* [Schema](https://docs.oasis-open.org/bioserv/BIAS/v2.0/csprd01/schemas/cbeff_ed2.xsd) 
* MOSIP's [CBEFF Utility](https://github.com/mosip/commons/tree/master/kernel/kernel-cbeffutil-api) to create, update, search and validate CBEFF XML data.

## CBEFF Sample

```markup
<?xml version="1.0" encoding="UTF-8"?>
<BIR xmlns="http://standards.iso.org/iso-iec/19785/-3/ed-2/">
   <BIRInfo>
      <Integrity>false</Integrity>
   </BIRInfo>
   <!-- right index finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.209Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Right IndexFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- right middle finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Right MiddleFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- right ring finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Right RingFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- right little finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Right LittleFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left index finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Left IndexFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left middle finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Left MiddleFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left ring finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Left RingFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left little finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Left LittleFinger</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- right thumb finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Right Thumb</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left thumb finger -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Finger</Type>
         <Subtype>Left Thumb</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- face -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Face</Type>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- right iris -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Iris</Type>
         <Subtype>Right</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
   <!-- left iris -->
   <BIR>
      <Version>
         <Major>1</Major>
         <Minor>1</Minor>
      </Version>
      <CBEFFVersion>
         <Major>1</Major>
         <Minor>1</Minor>
      </CBEFFVersion>
      <BIRInfo>
         <Integrity>false</Integrity>
      </BIRInfo>
      <BDBInfo>
         <Format>
            <Organization>Mosip</Organization>
            <Type>257</Type>
         </Format>
         <CreationDate>2019-06-27T13:40:06.211Z</CreationDate>
         <Type>Iris</Type>
         <Subtype>Left</Subtype>
         <Level>Raw</Level>
         <Purpose>Enroll</Purpose>
         <Quality>
            <Algorithm>
               <Organization>HMAC</Organization>
               <Type>SHA-256</Type>
            </Algorithm>
            <Score>100</Score>
         </Quality>
      </BDBInfo>
      <BDB>RklSAD...</BDB>
   </BIR>
</BIR>
```

