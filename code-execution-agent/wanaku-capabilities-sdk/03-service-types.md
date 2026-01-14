You are tasked with refactoring the ServiceTarget class and updating the service discovery API registration process. Make the following specific changes:

1. In the ServiceTarget class, rename the existing "service" field to "serviceName"

2. Remove the ServiceType enum from ServiceTarget and replace it with two new string fields:
   - serviceType (string)
   - serviceSubType (string)

3. Update the service registration process within the discovery API to accommodate these changes, ensuring that:
   - The registration endpoint accepts serviceName instead of service
   - The registration endpoint accepts both serviceType and serviceSubType as string values
   - All validation logic is updated to work with string-based service types rather than enum values
   - The data model for registered services reflects these new field names and types
   - Any queries or lookups in the discovery API use the updated field structure

4. Ensure backward compatibility is considered or document breaking changes if this is a major version update

5. Update any related documentation, API contracts, or interface definitions to reflect these structural changes
