1. Create PV
2. Create PVC
3. POD that uses the PVC--->PV
4. HostPat is support only single node only




-----------------------------------------
 KM :  If PV is 10Gi and PVC request 1Gi that mean lock 9Gi. That mean nobody can use PV anymore.

ReClaimPolicy : 
1. Retain : Data still be there.
2. Recycle : Druplicate 
3. Delete : Delete persistense data


Access Mode :
1. ReadWriteOne : It mean can read/write only one Node
2. ReadWriteMany : Mount on diference node
3. ReadOnly : nobody Node can read


Node: 
1. If not specify any node name. it will got some problem because pv type HostPath will be in the Node that the POD start
2. Solve by :
    - Under spec :  add  a few line below 
            nodeSelector
                demoserver  "true"

   -  kubectl label node kworker1.kubelab.loc demoserver="true"

