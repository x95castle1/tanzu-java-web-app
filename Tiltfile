load('.tanzu/tanzu_tilt_extensions.py', 'tanzu_k8s_yaml')


SOURCE_IMAGE = os.getenv("SOURCE_IMAGE", default='harbor-repo.vmware.com/tapsme/supply-chain/tanzu-java-web-app-source')
LOCAL_PATH = os.getenv("LOCAL_PATH", default='.')

custom_build('harbor-repo.vmware.com/tapsme/supply-chain/tanzu-java-web-app',
    "tanzu apps workload apply -f config/workload.yaml --live-update \
      --local-path " + LOCAL_PATH + " --source-image " + SOURCE_IMAGE + " --yes && \
    .tanzu/wait.sh tanzu-java-web-app",
  ['pom.xml', './target/classes'],
  live_update = [
    sync('./target/classes', '/workspace/BOOT-INF/classes')
  ],
  skips_local_docker=True
)

tanzu_k8s_yaml('tanzu-java-web-app', 'harbor-repo.vmware.com/tapsme/supply-chain/tanzu-java-web-app', './config/workload.yaml')
allow_k8s_contexts('unicorn-admin@unicorn')
