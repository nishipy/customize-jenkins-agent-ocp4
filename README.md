# Customize OpenShift jenkins agent image

## Build the image

### On RHEL host.
- RHELホスト上でビルドするとき、`subscription-manager`を使うと下記エラーが出る
	```
	STEP 6: RUN subscription-manager repos --enable=rhel-7-server-rpms     && subscription-manager repos --enable=rhel-7-server-extras-rpms     && subscription-manager repos --enable=rhel-7-server-optional-rpms
	subscription-manager is disabled when running inside a container. Please refer to your host system for subscription management.
	```
- 以下の手順で、ホストを登録
	```
	# subscription-manager register --username xxxx --password xxxxx --auto-attach
	# subscription-manager repos --enable=rhel-7-server-rpms
	# subscription-manager repos --enable=rhel-7-server-extras-rpms
	# subscription-manager repos --enable=rhel-7-server-optional-rpms
	```

### On not RHEL host.
- RHEL以外のホストでビルドするときは、一時的にDockerfileの中で、`subscription-manager register`すればいい

### On OpenShift 4
- カスタマーポータルからエンタイトルメント証明書をダウンロード[1]し、`on-ocp4/entitlement_certificates/`に配置
- パブリックキーとプライベートキーを別ファイルに分けて、シークレットとして登録[2]
	```
	$ oc create secret generic etc-pki-entitlement --from-file /path/to/entitlement/{ID}.pem \
	  --from-file /path/to/entitlement/{ID}-key.pem
	```

### 
## References
[1]:  https://access.redhat.com/documentation/ja-jp/red_hat_customer_portal/1/html/red_hat_network_certificate-based_subscription_management/index
[2]: https://access.redhat.com/documentation/ja-jp/openshift_container_platform/4.4/html/builds/builds-source-secrets-entitlements_running-entitled-builds
