# EgammaPostRecoTools

cmsrel CMSSW_12_6_0

cd CMSSW_12_6_0/src

cmsenv

git-cms-init

git-cms-addpkg RecoEgamma/PhotonIdentification

git-cms-addpkg RecoEgamma/ElectronIdentification

git-cms-addpkg RecoEgamma/EgammaTools

git-cms-addpkg EgammaAnalysis/ElectronTools

For Run3 Scales + smearing corrections :

The Run3 Scale and smearing files should be available here : EgammaAnalysis/ElectronTools/data/ScalesSmearings

The path to the correction file should be added here : https://github.com/Prasant1993/EgammaPostRecoTools/blob/Update_Run3ID_electronNoIso_MiniAOD/python/EgammaPostRecoTools.py#L117


For Run3 electron and photon IDs : 

The electron and photon ID config files should be changed in [1] and [2] :

[1] https://github.com/cms-sw/cmssw/tree/master/RecoEgamma/ElectronIdentification/python/Identification
[2] https://github.com/cms-sw/cmssw/tree/master/RecoEgamma/PhotonIdentification/python/Identification

In the analysis config file for producing ntuple, the follwing code block needs to be added :
                                                                                                              
from RecoEgamma.EgammaTools.EgammaPostRecoTools import setupEgammaPostRecoSeq

setupEgammaPostRecoSeq(process,

                       runEnergyCorrections=True,
		       
                       runVID=True,
		       
                       #era='2017-Nov17ReReco',                                                                                                                                                                    
                       #era='2017-UL',                                                                                                                                                                             
                       #era='2018-Prompt',                                                                                                                                                                         
                       #era='2018-UL',                                                                                                                                                                             
                       era='2022-Prompt',
		       
                       eleIDModules=['RecoEgamma.ElectronIdentification.Identification.cutBasedElectronID_Fall17_94X_V2_cff',

				     'RecoEgamma.ElectronIdentification.Identification.heepElectronID_HEEPV70_cff',
					
                                     'RecoEgamma.ElectronIdentification.Identification.mvaElectronID_Fall17_iso_V2_cff',
					
                                     'RecoEgamma.ElectronIdentification.Identification.mvaElectronID_Fall17_noIso_V2_cff',
					
                                     'RecoEgamma.ElectronIdentification.Identification.mvaElectronID_RunIIIWinter22_iso_V1_cff',
					
                                     'RecoEgamma.ElectronIdentification.Identification.mvaElectronID_RunIIIWinter22_noIso_V1_cff',
					
                                     'RecoEgamma.ElectronIdentification.Identification.cutBasedElectronID_Winter22_122X_V1_cff'],
					
                       phoIDModules=['RecoEgamma.PhotonIdentification.Identification.mvaPhotonID_Fall17_94X_V2_cff',
		       
                                     'RecoEgamma.PhotonIdentification.Identification.cutBasedPhotonID_Fall17_94X_V2_cff',
				     
                                     'RecoEgamma.PhotonIdentification.Identification.cutBasedPhotonID_RunIIIWinter22_122X_V1_cff',
				     
                                     'RecoEgamma.PhotonIdentification.Identification.mvaPhotonID_Winter22_122X_V1_cff']
                       )





In the final cms path we need to add "process.egammaPostRecoSeq" as well.

process.p = cms.Path( process.egammaPostRecoSeq * process.ggNtuplizer )