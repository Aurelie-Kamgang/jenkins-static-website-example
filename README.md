## jenkins-static-website-example

Continuous CI/CD deployment of a static web application on Jenkins.


### Prerequisites
 - Install docker 
 - install git
 - Have an account on the cloud provider Heroku
 - Install Jenkins

### Start
1. From Heroku get your token that will allow us to authenticate from outside:
**Account Settings -> API Key**
2. From Jenkins to authenticate on Heroku we have to set the environment variable HEROKU_API_KEY:
**Manage Jenkins -> Manage Credential -> Global -> Add credential -> secret text** 

![](https://lh3.googleusercontent.com/7Y59hqeMBHTVM1eUIFfTKLFWBL0Bnt-Be8BPaeEsMMhqHoniCqwGNUFlevkP3oBOWSlxTXxzj0nVLtw1Wa41bTfyQB7ZUDmBBacANNbLaT4x8D9TqS7iIoY9GVmmxxCn50DCw9cOqkug9lOQYoZ_ag6z0kYMsZCsvD2JEUdkMLiE0SLewqB0yG4KmA)

3. To get notifications on the status of the pipeline, we will link jenkins with the Slack messaging application.

- From Jenkins to authenticate on Slack we have to set the environment variable slack_token:
**Manage Jenkins -> Manage Credential -> Global -> Add credential -> secret text**

![](https://lh3.googleusercontent.com/7pvr8Lq9MpFM_ms36ygYrJoL1h5cf2HWiJrFYkX4Wpqbyi-CFMfqipjuLaV3_bO5szYb6ldE6vmpyhcxSlMClhP2bV1cuBbDt6t5fS4Rwh8jCLsbia6L92Hn75vTt2UMkxBnFELVGhDqzHROMzo_iJjPKx0o1vjqtrPwTpJ832VQMjaczRAB22h1QA)

4. Install the plugins:
- http_request: for http requests
- docker-build-step: to execute docker build and push commands
- slack-notification: For the messaging application
- Badge(Embeded status)

![](https://lh5.googleusercontent.com/g0vujbJyXRjL1jWLNdHTl8xlMpfAgEIygRu6T_pAnlohpDF90UkB0WtEYuCTx7mMMggnOsAE9g75rgQYRoh6hy8_769ZqA70YGBDdpiUaqt8bGAk8cJLkhP1uJuWbQIwXEPTb2ji0VCcB-TFvsPNLxsc9Bjb3ezWOPY1PWa_zapZFVwNnFDbgOfjOg)

5. Configure the system:
Go to : **Manage Jenkins -> Configure System -> Docker Build**
- Value:
**unix:///var/run/docker.sock**

![](https://lh4.googleusercontent.com/BEcO7D0p8IoiFSqJqr9Nfm6cSB-cP4PmakDEFz7MyDSvfW-pq5XbzUKkuATurab2f66YZ9oDF63BHCNEva6LZxOCb6RVqvFBZabyX6cCyJX44gK1Mt_jCnKTHbpTG5G1k3lj-3Q9e_qe97nXjVPiq0AN9GhQd2lOF_B1gyLVHU4vy4sGDucyyTPgCw)

**Manage Jenkins -> Configure System -> Slack**
![](https://lh3.googleusercontent.com/DDnoswMynkoSjlUZfwd49_smmoS5NLKVZuhX4Dsggak7CXaBvvVbUfHnInViyiTa7UMpR4eN-xrYKQxuZGpQg_xxz3r973b12B_KjM6auIMobFoaZhlEN8iAEmD3Bu7BpbeCFiZJOb85tFP4zXDC-ljB4UzBhmc--jz1EztwfnPws5-uJ9IxDc4mNQ)

NB: On the slack channel integrate jenkins-ci (slack-> application -> Jenkins-ci -> Integrate -> channel_name)

![](https://lh3.googleusercontent.com/qv95zomPH2ZzEIuJSalkNuAD6Qup3xwtjsVz3mQsaw-u1wlJrkIpDKQynQmRq-BEExFrmOXARoMsLinab6KVWYs5c4dz-wpfQ1I15LWjM8qWabfFXB5xHCCDdr3IHOXYQ1cQdC4FSBuQ1zAr35maNHvJtYmsUXfOxa49mJBzl4ueUVpWIEgDmslSOw)

6. Webhook: notifications about code changes on the repo will be sent by him.
To link our Jenkins to the webhook of our repos:
**- Go to repos -> Settings -> Webhook -> Add Webhook**

![](https://lh6.googleusercontent.com/6xFcT8aEM2c9mvdkjdykAYGRp30sotPuHNxEIOo2ic7eW6uB1-nLZpeHovQzGuM6jUAOSEFZ2bv0-2eGC78zRJf1UfjXriJdgxYN1T_EYoSfAOKbpzhaIT0p4ZPh3FLn_iNWRbwr-qLVxQdBuZBVEJh-YXvwUp17VhXXu-WkastYozRESLVn3uO-tA)

![](https://lh6.googleusercontent.com/QAP3EywmDu2Yda1KPfICRWsnRu4l5kzcW_LWPMXAwIgyfrSaJABfm-n632sL1EvPWGfRrH5rzqykK_l_Rqk1d8ZHuu_4riczumyYRk311npcxGhi_A0xB7BkCZp8PU9yRbgqSLT8aNYMCze3i0Uc6xqNTTV8-1iretyV1Eu3oINk3qj087q8lXEAjw)

![](https://lh4.googleusercontent.com/7l1-ouFDvFoXmlmO2L_Npz-kgH_M-wFtflDD6qFKrhGCv-lNiUiIPl8lvglCsGxoD3QeRADHM71WOdorfp1Ti1p8PS_aFGMPd0_oNVZ9Q4uPbhksGQOvkQ0kLWRcZ4Mg1YF9vc9yjDotiwucZhu6BSN3Ttsfiib-Te-rbb6HvOQ6Bi9K8pfzDpJKSA)

7. Create and launch Pipeline static-webapp

- Create:***New item*** 

![](https://lh5.googleusercontent.com/VGA-tbQbEvIIde0kvwhHufDyHisp68ARDwMssen6fYUQ8zN5e0oGGY6He85F2Ew0iSpiAmagNqlxpPxD9EozFkZcdExcCy8ZTMRqIXbu6H9_rAD0y_7tOGApP3HOzRW4fNp3qJ_PtPgywFsrjHqDW6skRU-rxD6TiJ3Wgd96Ocz6jwD4AeUrHK_JZw)

![](https://lh5.googleusercontent.com/ASA-MlEF35XAHPJEWkYeCNxBJyyNrjDM3OT1JIoF6y1zLNdRQNgtvL_nX36tkhqa9gyPieMUQjJaUP8U7PZhJVz_lG-ZhDM1Gdfb7MKB-l5yVOm57k3OrqZHZ3LpiVu_YLrVDfH9cLqYLrNl7mtM-KzjbxBXEu1P35fwlAdAazxIqtmyrHiVDU2IbQ)

![](https://lh6.googleusercontent.com/iO287dqzH5xN9EfaRz6tdAu44_ohZssecW2ffW0CR7HHfxqwQLxFNapWjmhmhaUwbxGWgv1MSTs9mdmIVcq-mQcCevm0EW4xksTaN7SfGOCluApmlFQfeMJ35qRbVWSzNnmGSiDyAS64Ff8Bdriy-6HlRqIuJRKIZcQZUq09jcPJsT3zyURG33cOmg)

- Launch: ***Build Now***

![](https://lh4.googleusercontent.com/4_0-KIzsIfT2obLUwz5gj-PNQ9S1XX7jsrJvVRGy7KrcOmXw5iSDHd0MuI_xsxpVYsWU4acWSlcEuNJRvbFNI4_3HkgTZV48u4LzhLCe3-Bhb4BkhKjarzgcUwn1VBTVuUqAImXIAX_amtK-cJ6FbsgGX1aTwRG0fX0KMUQnNvALdIZPwq7XPUpu4w)

![](https://lh6.googleusercontent.com/ABeT-o-HlIGx37MV5DF7fkuMu3OOOFJ8Jxyoi4_NyZvmFg721l2uur8IU4PCBHxGpn60kaqhGrW9M7s6w2ilEGit9zh6XucIlMGe1jpPFhLlPHYEKe6chRHzcokjUGT-SmvEXLvv9j4OjRI22JkuB-yAK7SAhywRQdiAmfzYqBURY624WRJ_CXLBDA)

