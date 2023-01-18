# Evaluation

- **Status:** Accepted
- **Application Document:** https://github.com/w3f/Grants-Program/blob/master/applications/social_recovery_wallet.md
- **Milestone:** 2
- **Kusama Identity:** Address
- **Previously successfully merged evaluation:** All by takahser

| Number | Deliverable | Accepted | Link | Evaluation Notes |
| ------ | ----------- | -------- | ---- |----------------- |
| 0a. | License | <ul><li>[x] </li></ul> | [MIT License](https://github.com/hypha-dao/hashed-wallet/blob/08b3414fa44de6a25d50338d77000f61598f9899/LICENSE) | - |
| 0b. | Documentation | <ul><li>[x] </li></ul> | [Tutorial](https://github.com/hypha-dao/hashed-wallet/blob/08b3414fa44de6a25d50338d77000f61598f9899/documentation/tutorial.md), [Flutter app repo](https://github.com/hypha-dao/hashed-wallet/tree/08b3414fa44de6a25d50338d77000f61598f9899), [Architecture doc](https://github.com/hypha-dao/hashed-wallet/blob/08b3414fa44de6a25d50338d77000f61598f9899/documentation/architecture.md) | Though not all of the code has inline comments, the important chunks are well documented - a good combo between clean self-documenting code and inline comments, where additional information is neccessary. |
| 0c. | Testing Guide | <ul><li>[x] </li></ul> | [Testing guide](https://github.com/hypha-dao/hashed-wallet/blob/08b3414fa44de6a25d50338d77000f61598f9899/documentation/testing_guide.md) | See [Testing Feedback](#testing-feedback) |
| 0d. | App Binaries | <ul><li>[x] </li></ul> | [APK for Android](https://github.com/hypha-dao/hashed-wallet/releases/tag/1.0.0_M2), [Android Testing Track](https://play.google.com/apps/internaltest/4701631300800602818), [iOS Testflight App](https://testflight.apple.com/join/NKhGqqxE) | We will provide an APK for Android and deliver the app on both Android and iOS platforms via the respective testing tracks in the Google Play and Apple App stores. |
| 0e. | Video | <ul><li>[x] </li></ul> | [Video Presentation](https://github.com/hypha-dao/hashed-wallet/blob/08b3414fa44de6a25d50338d77000f61598f9899/documentation/videos/milestone_2_delivery.md) | - |
| 1. | Recovery Lookup | <ul><li>[x] </li></ul> | [Flutter app repo](https://github.com/hypha-dao/hashed-wallet/tree/08b3414fa44de6a25d50338d77000f61598f9899) | Guardians can be added by the wallet owner (successfully smoke-tested). When in recovery mode, an info popup is shown with the ability to abort the process to the recovered account when the app is opened. Hence, the wallet can't be used when in recovery mode. |
| 2. | Vouch | <ul><li>[x] </li></ul> | [Flutter app repo](https://github.com/hypha-dao/hashed-wallet/tree/08b3414fa44de6a25d50338d77000f61598f9899) | The ability to vouch for user that has an active recovery requesting signature from the account in the wallet: successfully smoke-tested  |  
| 3. | Claim and Recover | <ul><li>[x] </li></ul> | [Flutter app repo](https://github.com/hypha-dao/hashed-wallet/tree/08b3414fa44de6a25d50338d77000f61598f9899) | When threshold is met, user will have the ability to claim and recover their tokens: successfully smoke-tested  |  

Ideally all links inside the above table should include the commit hash,
which was used for testing the delivery. It should also be checked if the software is published under the correct open-source license.

## General Notes

Summarizes the overall performance plus additional feedback/comments

### Testing Feedback

- Functionality was smoke-tested successfully. Initially, there was a bug with recovering an account when copy-pasting the mnemonic into the app, which the grantee resolved very quickly. The communication was great and the fix was published to the Apple Test Flight very soon after contacting them.
- Tests pass, however, as in M1 it was initially unclear which tests exactly ran. Also, it seemed like only the _mnemonic_test.dart_ test suite ran, which contains 2 tests. In contrast, _user_input_number_formatter_test.dart_ which contained much more tests was missing in the output. Finally, _old/utils/polkadot_test.dart_ tests was in the _old_ folder and I wondered if they were supposed to be run and even were supposed to be be removed.

    ```bash
    $ docker build --progress=plain -t flutterdocker .

    (...)

    Step 25/25 : RUN cd hashed-wallet && flutter test -r expanded
    ---> Running in 272111b38f02
    "es": 16 untranslated message(s).
    "he": 116 untranslated message(s).
    "pt": 62 untranslated message(s).
    To see a detailed report, use the untranslated-messages-file 
    option in the l10n.yaml file:
    untranslated-messages-file: desiredFileName.txt
    <other option>: <other selection> 


    This will generate a JSON format file containing all messages that 
    need to be translated.
    Running "flutter pub get" in hashed-wallet...                       9.1s
    00:00 +0: /home/user/hashed-wallet/test/account_service_test.dart: Test loadAccounts saveAccounts
    00:00 +1: /home/user/hashed-wallet/test/old/utils/polkadot_test.dart: polkadot JS load JS code
    00:00 +2: /home/user/hashed-wallet/test/old/utils/polkadot_test.dart: polkadot JS load JS code
    00:00 +3: /home/user/hashed-wallet/test/old/utils/polkadot_test.dart: polkadot JS load JS code
    00:00 +4: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: mnemonic decode mnemonic
    mnemonic: catch-story-inform-apple-above
    secret: 4d31c4a2db4120f4fc18c8ebf6e9e9f558166f5fa4c3d52bf202139f496604b0
    secret2: 4d31c4a2db4120f4fc18c8ebf6e9e9f558166f5fa4c3d52bf202139f496604b0
    00:00 +5: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +6: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +7: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +8: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +9: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +10: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +11: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +12: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +13: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +14: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +15: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +16: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +17: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +18: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +19: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:00 +20: /home/user/hashed-wallet/test/old/utils/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    00:01 +21: /home/user/hashed-wallet/test/time_remaining_timer_test.dart: test time remaining
    00:01 +22: All tests passed!
    Removing intermediate container 272111b38f02
    ---> 78c266a73c43
    Successfully built 78c266a73c43
    Successfully tagged flutterdocker:latest
    ```

    - However, these problems got fixed and the outputs are more clear abuot which tests ran. Also, the tests being run seem more appropriate:


    ```bash
    % docker build --progress=plain -t flutterdocker .

    (...)

    #22 [test 3/3] RUN cd hashed-wallet && flutter test -r expanded
    #22 sha256:65c1f8c343a6c7b5bcd7d589352c1ef2f67421f4f03e2a01a249228a0750381c
    #22 0.775 "es": 16 untranslated message(s).
    #22 0.776 "he": 116 untranslated message(s).
    #22 0.776 "pt": 62 untranslated message(s).
    #22 0.776 To see a detailed report, use the untranslated-messages-file 
    #22 0.776 option in the l10n.yaml file:
    #22 0.776 untranslated-messages-file: desiredFileName.txt
    #22 0.776 <other option>: <other selection> 
    #22 0.776 
    #22 0.776 
    #22 0.776 This will generate a JSON format file containing all messages that 
    #22 0.776 need to be translated.
    #22 0.807 Running "flutter pub get" in hashed-wallet...                      18.2s
    #22 35.18 00:00 +0: /home/user/hashed-wallet/test/time_remaining_timer_test.dart: test time remaining
    #22 35.53 00:00 +1: /home/user/hashed-wallet/test/account_service_test.dart: Test loadAccounts saveAccounts
    #22 35.55 00:00 +2: /home/user/hashed-wallet/test/account_service_test.dart: Test createAccount
    #22 35.56 00:00 +3: /home/user/hashed-wallet/test/account_service_test.dart: Test getPrivateKeys, savePrivateKeys
    #22 35.75 00:00 +4: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 45 should return 45
    #22 35.77 00:00 +5: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 8, should return 8
    #22 35.77 00:00 +6: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: "", should return "" 
    #22 35.78 00:00 +7: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 69.9 should return 69.9
    #22 35.78 00:00 +8: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 69, should return 69.
    #22 35.78 00:00 +9: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 69.. should return 69.
    #22 35.79 00:00 +10: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 458,4 should return 458.4
    #22 35.79 00:00 +11: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 453,343,343.676, should return 453343343.676
    #22 35.79 00:00 +12: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 453,343,343.676 should return 453343343.676 
    #22 35.80 00:00 +13: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 453.343.343,676 should return 453343343.676 
    #22 35.81 00:00 +14: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 46..474,38493.3627,384 should return 46474384933627.384 
    #22 35.82 00:00 +15: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: "345,,,," , should return "345." 
    #22 35.83 00:00 +16: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 8746..474,38493.3627,384 should return 8746474384933627.384
    #22 35.83 00:00 +17: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 843.384, should return 843.384
    #22 35.83 00:00 +18: /home/user/hashed-wallet/test/user_input_number_formatter_test.dart: Input: 843.384. should return 843.384
    #22 36.11 00:00 +19: /home/user/hashed-wallet/test/mnemonic_test.dart: mnemonic decode mnemonic
    #22 36.14 mnemonic: shoulder-flock-rule-hello-about
    #22 36.14 secret: d8ee2d6370990cb264718a4dd9d6d787ccc2fa49fd61199531592bbe5d51ae21
    #22 36.14 secret2: d8ee2d6370990cb264718a4dd9d6d787ccc2fa49fd61199531592bbe5d51ae21
    #22 36.14 00:00 +20: /home/user/hashed-wallet/test/mnemonic_test.dart: Seeds Global Passport Mnemonic Convert words from Seeds Global Passport
    #22 36.59 00:01 +21: All tests passed!
    #22 DONE 37.2s
    ```