# Shannon Pixel nvitem enabler scripts

This repository contains scripts that can be run on **rooted** Shannon-based Pixel devices to enable modem features which are off by default.

Some of these features may not work, may be buggy, or could crash your modem entirely.

> _Warning_
>
> Please only use the scripts made for your device. These nvitems are not the same across different devices, and what works on one may not work on another.
>
> If you end up in a non-usable modem state, you can [wipe all custom nvitems](#clear-custom-nvitems) and try again.

## How to use

1. Your device must be **rooted**. If it's not, this won't work. If you want to root your device, look elsewhere for a guide.
2. You must close any apps that might be using the modem's diagnostics port, like Network Signal Guru. It might take a minute for any app to close its connection to the modem completely.
3. Spawn an on-device shell via ADB: `adb shell`
4. Enter superuser mode: `su`
5. Copy and paste the contents of any script for your device and execute it.
6. You should see various "OK" messages in response. If you don't the commands won't have taken any effect.
7. Reboot your device for the changes to take effect. (You can do this from the shell using `reboot`.)

## Clear custom nvitems

To clear custom nvitems, use the [script provided](./clear_nvitems.sh) in a root ADB shell, then reboot:

```bash
# Spawn ADB shell over USB
adb shell

# Use root
su

# Back up custom nvitems
mv /mnt/vendor/efs/nv_normal.bin /mnt/vendor/efs/nv_normal.bin.old
mv /mnt/vendor/efs/nv_normal.bin.md5 /mnt/vendor/efs/nv_normal.bin.md5.old

# Reboot the device
reboot
```

## Changes

As an example, here's the differences in a UE capability response on a Pixel 7 Pro connected to EE UK.

```patch
***************
*** 1,4 ****
! TickTime : 202.694
  Exy LTE RRC OTA Packet
   Direction : Uplink
  ul-dcch
--- 1,4 ----
! TickTime : 429.345
  Exy LTE RRC OTA Packet
   Direction : Uplink
  ul-dcch
***************
*** 24,31 ****
          profile0x0104-r15 : false
         maxNumberROHC-ContextSessions : cs24
        phyLayerParameters
!        ue-TxAntennaSelectionSupported : false
!        ue-SpecificRefSigsSupported : false
        rf-Parameters
         supportedBandListEUTRA
          [0]
--- 24,31 ----
          profile0x0104-r15 : false
         maxNumberROHC-ContextSessions : cs24
        phyLayerParameters
!        ue-TxAntennaSelectionSupported : true
!        ue-SpecificRefSigsSupported : true
        rf-Parameters
         supportedBandListEUTRA
          [0]
***************
*** 435,444 ****
            EUTRA RRC_CONNECTED to UTRA TDD CELL_DCH PS handover : not supported
            UTRAN TDD measurements, reporting and measurement reporting event B2 in E-UTRA connected mode : not supported
            EUTRA RRC_CONNECTED to UTRA TDD CELL_DCH CS handover : not supported
!           Measurement reporting event: Event B1 - Neighbour > threshold for UTRAN FDD : not supported
            DCI format 3a : not supported
           nonCriticalExtension
            nonCriticalExtension
             nonCriticalExtension
              nonCriticalExtension
               nonCriticalExtension
--- 435,447 ----
            EUTRA RRC_CONNECTED to UTRA TDD CELL_DCH PS handover : not supported
            UTRAN TDD measurements, reporting and measurement reporting event B2 in E-UTRA connected mode : not supported
            EUTRA RRC_CONNECTED to UTRA TDD CELL_DCH CS handover : not supported
!           Measurement reporting event: Event B1 - Neighbour > threshold for UTRAN FDD : supported
            DCI format 3a : not supported
           nonCriticalExtension
            nonCriticalExtension
+            phyLayerParameters-v9d0
+             tm5-FDD-r9 : supported
+             tm5-TDD-r9 : supported
             nonCriticalExtension
              nonCriticalExtension
               nonCriticalExtension
***************
*** 1016,1021 ****
--- 1019,1048 ----
           ue-Category-v1020 : 7
           phyLayerParameters-v1020
            tm9-With-8Tx-FDD-r10 : supported
+           crossCarrierScheduling-r10 : supported
+           simultaneousPUCCH-PUSCH-r10 : supported
+           multiClusterPUSCH-WithinCC-r10 : supported
+           nonContiguousUL-RA-WithinCC-List-r10
+            [0]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [1]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [2]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [3]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [4]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [5]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [6]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [7]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [8]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
+            [9]
+             nonContiguousUL-RA-WithinCC-Info-r10 : supported
           rf-Parameters-v1020
            supportedBandCombination-r10
             [0]
***************
*** 3771,3793 ****
               [3]
                interRAT-NeedForGaps : true
           featureGroupIndRel10-r10
!           DMRS with OCC (orthogonal cover code) and SGH (sequence group hopping) disabling : not supported
!           Trigger type 1 SRS (aperiodic SRS) transmission (Up to X ports) : not supported
            PDSCH TM9 when up to 4 CSI reference signal ports are configured : supported
            PDSCH TM9 for TDD when 8 CSI reference signal ports are configured : supported
!           PUCCH RM2-0 when PDSCH TM9 is configured and RM2-1 when PDSCH TM9 and up to 4 CSI reference signal ports are configured : not supported
!           PUCCH RM2-1 when PDSCH TM9 and 8 CSI reference signal ports are configured : not supported
            PUSCH RM2-0 when PDSCH TM9 is configured and RM2-2 when PDSCH TM9 and up to 4 CSI reference signal ports are configured : not supported
!           PUSCH RM2-2 when PDSCH TM9 and 8 CSI reference signal ports are configured : not supported
!           PUCCH RM1-1 submode 1 : not supported
!           PUCCH RM1-1 submode 2 : not supported
            Measurement reporting trigger Event A6 : supported
            SCell addition within the Handover to EUTRA procedure : supported
            Trigger type 0 SRS (periodic SRS) transmission on X Serving Cells : supported
            Reporting of both UTRA CPICH RSCP and Ec/N0 in a Measurement Report : supported
!           Time domain ICIC RLM/RRM / ICIC RRM / ICIC CSI measurement sf restriction for the serving cell / neighbour cells : not supported
            Relative transmit phase continuity for spatial multiplexing in UL : not supported
           nonCriticalExtension
            rf-Parameters-v1060
             supportedBandCombinationExt-r10
              [0]
--- 3798,3826 ----
               [3]
                interRAT-NeedForGaps : true
           featureGroupIndRel10-r10
!           DMRS with OCC (orthogonal cover code) and SGH (sequence group hopping) disabling : supported
!           Trigger type 1 SRS (aperiodic SRS) transmission (Up to X ports) : supported
            PDSCH TM9 when up to 4 CSI reference signal ports are configured : supported
            PDSCH TM9 for TDD when 8 CSI reference signal ports are configured : supported
!           PUCCH RM2-0 when PDSCH TM9 is configured and RM2-1 when PDSCH TM9 and up to 4 CSI reference signal ports are configured : supported
!           PUCCH RM2-1 when PDSCH TM9 and 8 CSI reference signal ports are configured : supported
            PUSCH RM2-0 when PDSCH TM9 is configured and RM2-2 when PDSCH TM9 and up to 4 CSI reference signal ports are configured : not supported
!           PUSCH RM2-2 when PDSCH TM9 and 8 CSI reference signal ports are configured : supported
!           PUCCH RM1-1 submode 1 : supported
!           PUCCH RM1-1 submode 2 : supported
            Measurement reporting trigger Event A6 : supported
            SCell addition within the Handover to EUTRA procedure : supported
            Trigger type 0 SRS (periodic SRS) transmission on X Serving Cells : supported
            Reporting of both UTRA CPICH RSCP and Ec/N0 in a Measurement Report : supported
!           Time domain ICIC RLM/RRM / ICIC RRM / ICIC CSI measurement sf restriction for the serving cell / neighbour cells : supported
            Relative transmit phase continuity for spatial multiplexing in UL : not supported
+          ue-BasedNetwPerfMeasParameters-r10
+           loggedMeasurementsIdle-r10 : supported
+           standaloneGNSS-Location-r10 : supported
           nonCriticalExtension
+           fdd-Add-UE-EUTRA-Capabilities-v1060
+            phyLayerParameters-v1060
+             pmi-Disabling-r10 : supported
            rf-Parameters-v1060
             supportedBandCombinationExt-r10
              [0]
***************
*** 3883,3894 ****
--- 3916,3936 ----
             nonCriticalExtension
              pdcp-Parameters-v1130
               pdcp-SN-Extension-r11 : supported
+              supportRohcContextContinue-r11 : supported
              phyLayerParameters-v1130
               crs-InterfHandl-r11 : supported
+              ePDCCH-r11 : supported
+              multiACK-CSI-Reporting-r11 : supported
+              ss-CCH-InterfHandl-r11 : supported
+              tdd-SpecialSubframe-r11 : supported
+              txDiv-PUCCH1b-ChSelect-r11 : supported
+              ul-CoMP-r11 : supported
              rf-Parameters-v1130
              measParameters-v1130
              interRAT-ParametersCDMA2000-v1130
              otherParameters-r11
+              powerPrefInd-r11 : supported
+              ue-Rx-TxTimeDiffMeasurements-r11 : supported
              nonCriticalExtension
               ue-Category-v1170 : 10
               nonCriticalExtension
***************
*** 3902,3907 ****
--- 3944,3955 ----
                nonCriticalExtension
                 ue-Category-v11a0 : 12
                 nonCriticalExtension
+                 phyLayerParameters-v1250
+                  e-HARQ-Pattern-FDD-r12 : supported
+                  enhanced-4TxCodebook-r12 : supported
+                  pusch-FeedbackMode-r12 : supported
+                  noResourceRestrictionForTTIBundling-r12 : supported
+                  discoverySignalsInDeactSCell-r12 : supported
                  rf-Parameters-v1250
                   supportedBandListEUTRA-v1250
                    [0]
***************
*** 3933,3958 ****
--- 3981,4043 ----
                    [9]
                     dl-256QAM-r12 : supported
                   freqBandPriorityAdjustment-r12 : supported
+                 rlc-Parameters-r12
+                  extended-RLC-LI-Field-r12 : supported
                  ue-CategoryDL-r12 : 12
                  ue-CategoryUL-r12 : 13
                  measParameters-v1250
+                  timerT312-r12 : supported
+                  alternativeTimeToTrigger-r12 : supported
+                  incMonEUTRA-r12 : supported
+                  incMonUTRA-r12 : supported
                   extendedMaxMeasId-r12 : supported
+                  extendedRSRQ-LowerRange-r12 : supported
+                  rsrq-OnAllSymbols-r12 : supported
+                  csi-RS-DiscoverySignalsMeas-r12 : supported
                  nonCriticalExtension
                   ue-CategoryDL-v1260 : 16
                   nonCriticalExtension
                    nonCriticalExtension
+                    phyLayerParameters-v1280
+                     alternativeTBS-Indices-r12 : supported
                     nonCriticalExtension
                      pdcp-Parameters-v1310
+                      pdcp-SN-Extension-18bits-r13 : supported
                      rlc-Parameters-v1310
+                      extendedRLC-SN-SO-Field-r13 : supported
+                     mac-Parameters-v1310
+                      extendedMAC-LengthField-r13 : supported
+                      extendedLongDRX-r13 : supported
+                     phyLayerParameters-v1310
+                      codebook-HARQ-ACK-r13 : '01'B(1)
+                      crossCarrierScheduling-B5C-r13 : supported
+                      fdd-HARQ-TimingTDD-r13 : supported
+                      pucch-Format4-r13 : supported
+                      pucch-Format5-r13 : supported
+                      pucch-SCell-r13 : supported
+                      spatialBundling-HARQ-ACK-r13 : supported
+                      supportedBlindDecoding-r13
+                       maxNumberDecoding-r13 : 1
+                       pdcch-CandidateReductions-r13 : supported
+                       skipMonitoringDCI-Format0-1A-r13 : supported
+                      uci-PUSCH-Ext-r13 : supported
+                      crs-InterfMitigationTM10-r13 : supported
+                      pdsch-CollisionHandling-r13 : supported
                      rf-Parameters-v1310
                       eNB-RequestedParameters-r13
                        requestedCCsDL-r13 : 5
                        requestedCCsUL-r13 : 2
                       maximumCCsRetrieval-r13 : supported
                       skipFallbackCombinations-r13 : supported
+                     measParameters-v1310
+                      rs-SINR-Meas-r13 : supported
                      interRAT-ParametersWLAN-r13
                      laa-Parameters-r13
+                      crossCarrierSchedulingLAA-DL-r13 : supported
+                      csi-RS-DRS-RRM-MeasurementsLAA-r13 : supported
                       downlinkLAA-r13 : supported
+                      endingDwPTS-r13 : supported
+                      secondSlotStartingPosition-r13 : supported
                      wlan-IW-Parameters-v1310
                      lwip-Parameters-r13
                      nonCriticalExtension
***************
*** 3961,3973 ****
--- 4046,4377 ----
                        nonCriticalExtension
                         nonCriticalExtension
                          ce-Parameters-v1350
+                          unicastFrequencyHopping-r13 : supported
                          nonCriticalExtension
                           nonCriticalExtension
                            phyLayerParameters-v1430
+                            alternativeTBS-Index-r14 : supported
+                           mac-Parameters-v1430
+                            shortSPS-IntervalFDD-r14 : supported
+                            shortSPS-IntervalTDD-r14 : supported
+                            skipUplinkDynamic-r14 : supported
+                            skipUplinkSPS-r14 : supported
+                            multipleUplinkSPS-r14 : supported
+                            dataInactMon-r14 : supported
                            rlc-Parameters-v1430
                            rf-Parameters-v1430
+                            supportedBandCombination-v1430
+                             [0]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [1]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [2]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [3]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [4]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [5]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [6]
+                              bandParameterList-v1430
+                               [0]
+                             [7]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [8]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [9]
+                              bandParameterList-v1430
+                               [0]
+                             [10]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [11]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [12]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [13]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [14]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [15]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [16]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [17]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [18]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [19]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [20]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [21]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [22]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [23]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [24]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                             [25]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [26]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [27]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [28]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [29]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [30]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [31]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [32]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [33]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [34]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [35]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [36]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [37]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [38]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [39]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [40]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [41]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [42]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [43]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [44]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [45]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [46]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [47]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [48]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [49]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [50]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [51]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                             [52]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                               [2]
+                             [53]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
+                               [2]
+                             [54]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                               [2]
+                                ul-256QAM-r14 : supported
+                             [55]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-perCC-InfoList-r14
+                                 [0]
+                                  ul-256QAM-perCC-r14 : supported
+                                 [1]
+                                  ul-256QAM-perCC-r14 : supported
+                             [56]
+                              bandParameterList-v1430
+                               [0]
+                                ul-256QAM-r14 : supported
+                               [1]
+                             [57]
+                              bandParameterList-v1430
+                               [0]
+                               [1]
+                                ul-256QAM-r14 : supported
                             diffFallbackCombReport-r14 : supported
+                           laa-Parameters-v1430
+                            crossCarrierSchedulingLAA-UL-r14 : supported
+                            uplinkLAA-r14 : supported
+                            twoStepSchedulingTimingInfo-r14 : nPlus1
+                            uss-BlindDecodingAdjustment-r14 : supported
+                            uss-BlindDecodingReduction-r14 : supported
+                            outOfSequenceGrantHandling-r14 : supported
                            otherParameters-v1430
+                           mmtel-Parameters-r14
+                            delayBudgetReporting-r14 : supported
+                            pusch-Enhancements-r14 : supported
+                            recommendedBitRate-r14 : supported
+                            recommendedBitRateQuery-r14 : supported
                            ce-Parameters-v1430
                            nonCriticalExtension
                             lwa-Parameters-v1440
***************
*** 4062,4068 ****
--- 4466,4474 ----
                                 featureSetsUL-PerCC-r15
                                  [0]
                                   supportedMIMO-CapabilityUL-r15 : twoLayers
+                                  ul-256QAM-r15 : supported
                                  [1]
+                                  ul-256QAM-r15 : supported
                                pdcp-ParametersNR-r15
                                 rohc-Profiles-r15
                                  profile0x0001-r15 : false

```