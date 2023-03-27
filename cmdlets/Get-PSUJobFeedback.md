---
external help file: Universal.Cmdlets.dll-Help.xml
Module Name: Universal
online version: https://go.microsoft.com/fwlink/?LinkID=217032
schema: 2.0.0
---

# Get-PSUJobFeedback

## SYNOPSIS
Returns feedback requested by jobs.

## SYNTAX

### ById
```
Get-PSUJobFeedback -JobId <Int64> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByRunId
```
Get-PSUJobFeedback -RunId <Guid> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

### ByObject
```
Get-PSUJobFeedback -Job <Job> [-ComputerName <String>] [-AppToken <String>] [-UseDefaultCredentials]
 [-Integrated] [<CommonParameters>]
```

## DESCRIPTION
Returns feedback requested by jobs.

## EXAMPLES

### Example 1
```
PS C:\> Get-UAJobFeedback -JobId 10
```

Returns the feedback requested by job 10.

## PARAMETERS

### -AppToken
An app token to access the UA API.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ComputerName
The HTTP address of the UA REST API server.

```yaml
Type: String
Parameter Sets: (All)
Aliases: Uri

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Integrated
Executes the command internally rather than using the Management API. Only works when running script from within PowerShell Universal. 

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -Job
The job to return feedback for.

```yaml
Type: Job
Parameter Sets: ByObject
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: True (ByValue)
Accept wildcard characters: False
```

### -JobId
The job ID to return feedback for.

```yaml
Type: Int64
Parameter Sets: ById
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -UseDefaultCredentials
Use default credentials when connecting to the management API

```yaml
Type: SwitchParameter
Parameter Sets: (All)
Aliases:

Required: False
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -RunId
The run ID (GUID) for this job. Requires JobRunId experimental feature. 

```yaml
Type: Guid
Parameter Sets: ByRunId
Aliases:

Required: True
Position: Named
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters
This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable, -InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable, -Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### UniversalAutomation.Job
## OUTPUTS

### System.Object
## NOTES

## RELATED LINKS
