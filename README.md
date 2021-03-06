Project to demonstrate overriding application configuration and resource parameters in Service Fabric.
It also shows how to deploy multiple instances with different configurations for each instance.
This is helpful if you are going to share a Service Fabric cluster for multiple environments (Dev, Test, QA, etc.)

To deploy multiple instances and override the parameters, you can use the following PowerShell:
#######################################################################################################################################################################################################################################
$packagepath = "C:\Users\bobjac\Desktop\GitHub\servicefabricweboverride\src\Application1\Application1\pkg\Debug"

Connect-ServiceFabricCluster -ConnectionEndpoint "localhost:19000"

Copy-ServiceFabricApplicationPackage -ApplicationPackagePath $packagepath -ImageStoreConnectionString "file:C:\SfDevCluster\Data\ImageStoreShare" -ApplicationPackagePathInImageStore "Application1"

Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'Application1'

Get-ServiceFabricApplicationType

New-ServiceFabricApplication -ApplicationName 'fabric:/Application1' -ApplicationTypeName 'Application1Type' -ApplicationTypeVersion 2.0.0
New-ServiceFabricApplication -ApplicationName 'fabric:/Application2' -ApplicationTypeName 'Application1Type' -ApplicationTypeVersion 2.0.0 -ApplicationParameter @{Web1_Value1='ChaseUtley'; Web1_Value2='RyanHoward'; Port="8203"}
#######################################################################################################################################################################################################################################
