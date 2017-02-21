# 概要
## [Azure Portal プレビューとは](introduction/what-is-microsoft-intune.md)
## 作業開始
<!---(introduction/get-started.md) --->
### [無料試用版にサインアップ](introduction/sign-up-free-trial-microsoft-intune.md)
## [新機能](introduction/whats-new.md)
## [既知の問題](introduction/known-issues-in-the-intune-preview.md)
<!--- ## [Get support](introduction/get-support.md)
## [Related resources](introduction/related-resources.md)

## [Get started](plan-and-design/get-started.md) --->

# [計画と設計](/intune/plan-design/introduction?toc=%2fintune-azure%2ftoc.json)
## [セクション 1: 展開の目標、目的、課題を決定する](/intune/plan-design/section-1-determine-deployment-goals-objectives-challenges?toc=%2fintune-azure%2ftoc.json)
## [セクション 2: ユース ケース シナリオを特定する](/intune/plan-design/section-2-identify-use-case-scenarios?toc=%2fintune-azure%2ftoc.json)
## [セクション 3: ユース ケースのシナリオの要件を決定する](/intune/plan-design/section-3-determine-use-case-requirements?toc=%2fintune-azure%2ftoc.json)
## [セクション 4: ロールアウト計画を作成する](/intune/plan-design/section-4-develop-a-rollout-plan?toc=%2fintune-azure%2ftoc.json)
## [セクション 5: コミュニケーション計画を作成する](/intune/plan-design/section-5-develop-a-rollout-communication-plan?toc=%2fintune-azure%2ftoc.json)
## [セクション 6: サポート計画を作成する](/intune/plan-design/section-6-develop-a-support-plan?toc=%2fintune-azure%2ftoc.json)
## [セクション 7: Intune の設計を作成する](/intune/plan-design/section-7-create-an-intune-design?toc=%2fintune-azure%2ftoc.json)
## [セクション 8: Intune を実装する](/intune/plan-design/section-8-onboarding-process?toc=%2fintune-azure%2ftoc.json)
## [セクション 9: テストして検証する](/intune/plan-design/section-9-test-and-validation?toc=%2fintune-azure%2ftoc.json)
## [その他のリソース](/intune/plan-design/additional-resources?toc=%2fintune-azure%2ftoc.json)

# デバイスの登録
## [デバイスの登録とは](enroll-devices/what-is.md)
## 作業開始
### [MDM 機関を設定する](enroll-devices/set-mdm-authority.md)
## 計画と設計
### [Apple MDM プッシュ証明書を取得する](enroll-devices/get-an-apple-mdm-push-certificate.md)
### [Apple DEP トークンを取得する](enroll-devices/get-apple-dep-token.md)
### [iOS デバイスの登録方法を選択する](enroll-devices/choose-ios-enrollment-method.md)
## 方法
### [Android デバイスを登録する](enroll-devices/enroll-android-and-knox-standard-devices.md)
### iOS デバイスを登録する
#### [セットアップ アシスタントを使用して iOS デバイスを登録する](enroll-devices/enroll-ios-devices-with-apple-configurator-and-setup-assistant.md)
#### [直接登録を使用して iOS デバイスを登録する](enroll-devices/enroll-ios-devices-with-apple-configurator-and-direct-enrollment.md)
#### [Apple Configurator のシリアル番号を追加する](enroll-devices/add-apple-configurator-serial-numbers.md)
#### [デバイス登録プログラムを使用して iOS デバイスを登録する](enroll-devices/enroll-ios-devices-using-device-enrollment-program.md)
### [デバイス登録マネージャーを使用してデバイスを登録する](enroll-devices/enroll-devices-using-device-enrollment-manager.md)
### [macOS デバイスの登録](enroll-devices/enroll-macos-devices.md)
### [Windows デバイスの登録](enroll-devices/enroll-window-devices.md)
### デバイス登録を管理する
#### [使用条件を作成する](enroll-devices/create-terms-and-conditions.md)
#### [登録制限を設定する](enroll-devices/set-enrollment-restrictions.md)
#### [デバイスをグループにマッピングする](enroll-devices/how-to-use-device-group-mapping.md)
#### [企業 ID を追加する](enroll-devices/add-corporate-identifiers.md)
#### [Windows Hello for Business を使用する](enroll-devices/how-to-use-windows-hello.md)
<!--- ## [Troubleshoot](enroll-devices/troubleshooting.md) --->

# デバイスとグループ
## [デバイス管理とは](manage-devices/what-is.md)
<!--- ## [Get started](manage-devices/get-started.md) --->
<!--- ## [Plan and design](manage-devices/plan-and-design.md) --->
## 方法
### [フル ワイプまたは選択的ワイプを使用する](manage-devices/use-full-or-selective-wipe-on-devices-using-microsoft-intune.md)
<!--- ## [Troubleshoot](manage-devices/troubleshooting.md) --->

# ユーザーの管理
## [ユーザー管理とは](manage-users/what-is.md)
<!--- Was What is users & group management--->
## [作業開始](manage-users/get-started-with-groups.md)
<!--- ## [Plan and design](manage-users/plan-and-design.md) --->

<!--- ## [Troubleshoot](manage-users/troubleshooting.md) --->

# アプリを管理する
## [アプリ管理とは](manage-apps/what-is-app-management.md)
## [アプリ保護ポリシーとは](manage-apps/what-is-app-protection-policy.md)
<!--- ## [Get started](manage-apps/get-started.md)
## [Plan and design](manage-apps/plan-and-design.md) --->
## アプリを管理する方法
### [アプリを追加する](manage-apps/add-apps.md)
#### [Android の基幹業務アプリ](manage-apps/android-lob-app.md)
#### [Android ストア アプリ](manage-apps/android-store-app.md)
#### [iOS の基幹業務アプリ](manage-apps/ios-lob-app.md)
#### [iOS ストア アプリ](manage-apps/ios-store-app.md)
#### [Web アプリ](manage-apps/web-app.md)
#### [Windows Phone 8.1 ストア アプリ](manage-apps/windows-phone-8-1-store-app.md)
#### [Windows ストア アプリ](manage-apps/windows-store-app.md)
### [アプリを割り当てる](manage-apps/deploy-apps.md)
### [アプリの監視](manage-apps/monitor-apps.md)
### [アプリ構成ポリシーを使用する](manage-apps/app-configuration-policies.md)
### [選択的にワイプするアプリ](manage-apps/app-selective-wipe.md)
<!---Is this specific to app protection policy or more general app management?--->
### [ボリューム購入アプリを操作する](manage-apps/volume-purchased-apps.md)
#### [iOS VPP アプリ](manage-apps/ios-vpp-apps.md)
#### [ビジネス向け Windows ストアのアプリ](manage-apps/wsfb-apps.md)
### [ポータル サイト アプリを構成する](manage-apps/company-portal-app.md)
## アプリ保護ポリシーを使用する方法
### [アプリ保護ポリシーを作成して割り当てる](manage-apps/app-protection-policies.md)
#### [Android の設定](manage-apps/android-app-protection-policy-settings.md)
#### [iOS の設定](manage-apps/ios-app-protection-policy-settings.md)
### [アプリ保護ポリシーを確認する](manage-apps/validate-app-protection-policies.md)
### [アプリ保護のユーザーの状態を監視する](manage-apps/monitor-app-protection-policies-with-microsoft-intune.md)
### [iOS アプリ間のデータ転送を管理する](manage-apps/manage-data-transfer-between-ios-apps-with-microsoft-intune.md)
### [アプリ保護ポリシー付きの Android アプリ](manage-apps/app-protection-enabled-android-apps.md)
### [アプリ保護ポリシー付きの iOS アプリ](manage-apps/app-protection-enabled-ios-apps.md)


<!--- ##  [Troubleshoot apps](manage-apps/troubleshooting.md) --->

# デバイスの構成
## [デバイス プロファイルとは](configure-devices/what-are-device-profiles.md)
<!---## [Get started](configure-devices/get-started.md)
## [Plan and design](configure-devices/plan-and-design.md) --->
## 方法
### [デバイス プロファイルを構成する](configure-devices/how-to-create-device-profiles.md)
### [デバイス制限を構成する](configure-devices/how-to-configure-device-restrictions.md)
#### [Android](configure-devices/device-restrictions-for-android.md)
#### [iOS](configure-devices/device-restrictions-for-ios.md)
#### [macOS](configure-devices/device-restrictions-for-macos.md)
#### [Windows 8.1](configure-devices/device-restrictions-for-windows-8-1.md)
#### [Windows Phone 8.1](configure-devices/device-restrictions-for-windows-phone-8-1.md)
#### [Windows 10](configure-devices/device-restrictions-for-windows-10.md)
#### [Windows 10 Team](configure-devices/device-restrictions-for-windows-10-team.md)

### [電子メールの設定を構成する](configure-devices/how-to-configure-email-settings.md)
#### [Android](configure-devices/email-profile-settings-for-android.md)
#### [iOS](configure-devices/email-profile-settings-for-ios.md)
#### [Windows Phone 8.1](configure-devices/email-profile-settings-for-windows-phone-8-1.md)
#### [Windows 10](configure-devices/email-profile-settings-for-windows-10.md)

### [VPN の設定を構成する](configure-devices/how-to-configure-vpn-settings.md)
#### [Android](configure-devices/vpn-for-android.md)
#### [iOS](configure-devices/vpn-for-ios.md)
#### [macOS](configure-devices/vpn-for-macos.md)
#### [Windows 8.1](configure-devices/vpn-for-windows-8-1.md)
#### [Windows Phone 8.1](configure-devices/vpn-for-windows-phone-8-1.md)
#### [Windows 10](configure-devices/vpn-for-windows-10.md)

### [Wi-Fi の設定を構成する](configure-devices/how-to-configure-wi-fi-settings.md)
#### [Android](configure-devices/wi-fi-for-android.md)
#### [iOS](configure-devices/wi-fi-for-ios.md)
#### [macOS](configure-devices/wi-fi-for-macos.md)
#### [Windows 8.1 および Windows 10](configure-devices/wi-fi-import-for-windows-8-1.md)

### [Windows 10 エディションのアップグレード設定を構成する](configure-devices/how-to-configure-windows-10-edition-upgrade.md)
### [証明書を構成する](configure-devices/how-to-configure-certificates.md)
#### [SCEP](configure-devices/configure-certificate-infrastructure-for-scep.md)
#### [PKCS](configure-devices/configure-certificate-infrastructure-for-pfx.md)

### [Windows Information Protection 設定を構成する](configure-devices/how-to-configure-windows-information-protection.md)
<!--- ### [Configure iOS education settings](configure-devices/education-settings-for-ios.md) --->

### [カスタム設定を構成する](configure-devices/how-to-configure-custom-settings.md)
#### [Android](configure-devices/custom-for-android.md)
##### [事前共有キーを使用する Wi-Fi プロファイル](configure-devices/wi-fi-profile-with-shared-key.md)
##### [アプリごとの VPN プロファイル](configure-devices/per-app-vpn-for-android-pulse-secure.md)
##### [Samsung KNOX Standard 用アプリの許可/禁止](configure-devices/custom-policy-to-allow-and-block-samsung-knox-apps.md)
#### [iOS](configure-devices/custom-for-ios.md)
#### [macOS](configure-devices/custom-for-macos.md)
#### [Windows Phone 8.1](configure-devices/custom-for-windows-phone-8-1.md)
#### [Windows 10](configure-devices/custom-for-windows-10.md)

### [デバイス プロファイルを割り当てる](configure-devices/how-to-assign-device-profiles.md)
### [デバイス プロファイルを監視する](configure-devices/how-to-monitor-device-profiles.md)
### [通信費管理サービスをセットアップする](configure-devices/set-up-telecom-expense-management-service-in-microsoft-intune.md)
## [トラブルシューティング](configure-devices/troubleshoot-device-profiles.md)

# デバイス コンプライアンスの設定
## [デバイス コンプライアンスとは](set-device-compliance/what-is-device-compliance.md)
## [作業開始](set-device-compliance/get-started-with-device-compliance.md)
## 方法
### [Android コンプライアンス ポリシーを作成する](set-device-compliance/create-a-compliance-policy-for-android.md)
### [Android for Work コンプライアンス ポリシーを作成する](set-device-compliance/create-a-compliance-policy-for-android-for-work.md)
### [iOS コンプライアンス ポリシーを作成する](set-device-compliance/create-a-compliance-policy-for-ios.md)
### [Windows コンプライアンス ポリシーを作成する](set-device-compliance/create-a-compliance-policy-for-windows.md)
<!--- ### [Monitor device compliance](set-device-compliance/monitor-device-compliance.md)--->



# 条件付きアクセス
## [条件付きアクセスとは](conditional-access/what-is-conditional-access.md)
## 方法
### [Exchange On-premises Connector をインストールする](conditional-access/install-intune-on-premises-exchange-connector.md)
### [条件付きアクセス ポリシーを作成する](conditional-access/create-conditional-access-policy-for-exchange-on-premises.md)

# アクセス制御
## [ロールベースのアクセス制御とは](access-control/role-based-access-control.md)

# 開発とカスタマイズ
## [Intune アプリ ラッピング ツール](/intune/deploy-use/decide-how-to-prepare-apps-for-mobile-application-management-with-microsoft-intune?toc=%2fintune-azure%2ftoc.json)
### [iOS 用アプリ ラッピング ツール](/intune/deploy-use/prepare-ios-apps-for-mobile-application-management-with-the-microsoft-intune-app-wrapping-tool?toc=%2fintune-azure%2ftoc.json)
### [Android 用アプリ ラッピング ツール](/intune/deploy-use/prepare-android-apps-for-mobile-application-management-with-the-microsoft-intune-app-wrapping-tool?toc=%2fintune-azure%2ftoc.json)
## [Intune アプリ SDK](/intune/develop/intune-app-sdk?toc=%2fintune-azure%2ftoc.json)
## [Intune Graph API](https://graph.microsoft.io/docs/api-reference/beta/resources/intune_graph_overview)


<!--HONumber=Feb17_HO3-->

