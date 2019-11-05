# Skaffold bug

Skaffold fails when trying to run same deployment twice.

Failing version: 0.41.0
Working version: 0.40.0

```bash
chinmaya:bug-skaffold-run chinmaya$ brew list --versions skaffold
skaffold 0.41.0 0.40.0

chinmaya:bug-skaffold-run chinmaya$ brew switch skaffold 0.41.0
Cleaning /usr/local/Cellar/skaffold/0.41.0
Cleaning /usr/local/Cellar/skaffold/0.40.0
3 links created for /usr/local/Cellar/skaffold/0.41.0

chinmaya:bug-skaffold-run chinmaya$ 
chinmaya:bug-skaffold-run chinmaya$ skaffold run
Generating tags...
Checking cache...
Tags used in deployment:
Starting deploy...
 - job.batch/test-job created
You can also run [skaffold run --tail] to get the logs

chinmaya:bug-skaffold-run chinmaya$ 
chinmaya:bug-skaffold-run chinmaya$ skaffold run
Generating tags...
Checking cache...
Tags used in deployment:
Starting deploy...
 - The Job "test-job" is invalid: spec.template: Invalid value: core.PodTemplateSpec{ObjectMeta:v1.ObjectMeta{Name:"test-job", GenerateName:"", Namespace:"", SelfLink:"", UID:"", ResourceVersion:"", Generation:0, CreationTimestamp:v1.Time{Time:time.Time{wall:0x0, ext:0, loc:(*time.Location)(nil)}}, DeletionTimestamp:(*v1.Time)(nil), DeletionGracePeriodSeconds:(*int64)(nil), Labels:map[string]string{"app.kubernetes.io/managed-by":"skaffold-v0.41.0", "controller-uid":"146c62e0-000d-11ea-b6e7-005056b9ecd8", "job-name":"test-job", "skaffold.dev/builder":"local", "skaffold.dev/cleanup":"true", "skaffold.dev/deployer":"kustomize", "skaffold.dev/docker-api-version":"1.40", "skaffold.dev/run-id":"57674785-0062-43d9-ab56-e7d8c008dfe5", "skaffold.dev/tag-policy":"git-commit", "skaffold.dev/tail":"true"}, Annotations:map[string]string(nil), OwnerReferences:[]v1.OwnerReference(nil), Initializers:(*v1.Initializers)(nil), Finalizers:[]string(nil), ClusterName:"", ManagedFields:[]v1.ManagedFieldsEntry(nil)}, Spec:core.PodSpec{Volumes:[]core.Volume(nil), InitContainers:[]core.Container(n
il), Containers:[]core.Container{core.Container{Name:"job", Image:"bash", Command:[]string{"echo", "Hello World"}, Args:[]string(nil), WorkingDir:"", Ports:[]core.ContainerPort(nil), EnvFrom:[]core.EnvFromSource(nil), Env:[]core.EnvVar(nil), Resources:core.ResourceRequire
ments{Limits:core.ResourceList(nil), Requests:core.ResourceList(nil)}, VolumeMounts:[]core.VolumeMount(nil), VolumeDevices:[]core.VolumeDevice(nil), LivenessProbe:(*core.Probe)(nil), ReadinessProbe:(*core.Probe)(nil), Lifecycle:(*core.Lifecycle)(nil), TerminationMessagePa
th:"/dev/termination-log", TerminationMessagePolicy:"File", ImagePullPolicy:"Always", SecurityContext:(*core.SecurityContext)(nil), Stdin:false, StdinOnce:false, TTY:false}}, RestartPolicy:"Never", TerminationGracePeriodSeconds:(*int64)(0xc011045d58), ActiveDeadlineSecond
s:(*int64)(nil), DNSPolicy:"ClusterFirst", NodeSelector:map[string]string(nil), ServiceAccountName:"", AutomountServiceAccountToken:(*bool)(nil), NodeName:"", SecurityContext:(*core.PodSecurityContext)(0xc017226150), ImagePullSecrets:[]core.LocalObjectReference(nil), Hostname:"", Subdomain:"", Affinity:(*core.Affinity)(nil), SchedulerName:"default-scheduler", Tolerations:[]core.Toleration(nil), HostAliases:[]core.HostAlias(nil), PriorityClassName:"", Priority:(*int32)(nil), DNSConfig:(*core.PodDNSConfig)(nil), ReadinessGates:[]core.PodReadinessGate(nil), RuntimeClassName:(*string)(nil), EnableServiceLinks:(*bool)(nil)}}: field is immutable
FATA[0000] kubectl error: kubectl apply: exit status 1

chinmaya:bug-skaffold-run chinmaya$ 
chinmaya:bug-skaffold-run chinmaya$ brew switch skaffold 0.40.0
Cleaning /usr/local/Cellar/skaffold/0.41.0
Cleaning /usr/local/Cellar/skaffold/0.40.0
3 links created for /usr/local/Cellar/skaffold/0.40.0

chinmaya:bug-skaffold-run chinmaya$ skaffold run
Generating tags...
Tags generated in 46.748µs
Checking cache...
Cache check complete in 25.258µs
Tags used in deployment:
Starting deploy...
 - job.batch/test-job configured
Deploy complete in 2.244784367s
You can also run [skaffold run --tail] to get the logs
There is a new version (0.41.0) of Skaffold available. Download it at https://storage.googleapis.com/skaffold/releases/latest/skaffold-darwin-amd64
```