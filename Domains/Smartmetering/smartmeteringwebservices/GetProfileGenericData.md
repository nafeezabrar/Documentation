## GetProfileGenericData request

### Description
GetProfileGenericData is a request to retrieve any DLMS "Profile generic" data from an E-meter. The request needs the DeviceIdentification.

The specific Profile generic data to be retrieved is identified by its OBIS code included as ObisCode according to the ObisCodeValues as specified in [common.xsd](https://github.com/OSGP/Shared/blob/development/osgp-ws-smartmetering/src/main/resources/schemas/common.xsd).

Selective access will be applied as described in the DLMS standard for access selector *range_descriptor*.
The clock definition is used as *restricting_object*. The *from_value* and *to_value* for the captured clock values will be set based on the BeginDate and EndData in the request.

It is possible to further reduce the amount of data retrieved from the device to specify *selected_values*. This is done by including the optional SelectedValues element in the request specifying one or more capture object definitions as CaptureObject according to the CaptureObjectDefinition in [common.xsd](https://github.com/OSGP/Shared/blob/development/osgp-ws-smartmetering/src/main/resources/schemas/common.xsd).

The clock definition must not be specified in the SelectedValues, since it will always be included in the results. The values that are specified must be capture object definitions that appear in the list of *capture_objects* for the Profile generic data that is retrieved.

All requests have similar response behaviour which is described in [ResponseMessages](./ResponseMessages.md).

The ultimately returned response for the GetProfileGenericData request is as specified in [GetProfileGenericDataResponse](./GetProfileGenericDataResponse.md).

### References

XSD: [sm-monitoring.xsd](https://github.com/OSGP/Shared/blob/development/osgp-ws-smartmetering/src/main/resources/schemas/sm-monitoring.xsd)

WSDL: [SmartMeteringMonitoring.wsdl](https://github.com/OSGP/Shared/blob/development/osgp-ws-smartmetering/src/main/resources/SmartMeteringMonitoring.wsdl)
