---
description: Charting components for Universal Dashboard.
---

# Charts

Universal Dashboard provides several built-in charting solutions to help visualize your data retrieved from PowerShell.

## ChartJS

Universal Dashboard integrates with [ChartJS](https://www.chartjs.org/).

### Creating a Chart

To create a chart, use `New-UDChartJS` and `New-UDChartJSData`. The below chart shows the top ten CPU using processes.

![](<../../../../.gitbook/assets/image (157) (1) (2) (2) (2) (2) (1) (1) (1) (1) (1) (1) (1).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

### Types

#### Bar

![](<../../../../.gitbook/assets/image (157) (1) (2) (2) (2) (2) (1) (1) (1) (1) (1) (1).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Stacked Bar

```powershell
    $GraphPrep = @(
        @{ RAM = "Server1"; AvailableRam = 128; UsedRAM = 10 }
        @{ RAM = "Server2"; AvailableRam = 64; UsedRAM = 63 }
        @{ RAM = "Server3"; AvailableRam = 48; UsedRAM = 40 }
        @{ RAM = "Server4"; AvailableRam = 64;; UsedRAM = 26 }
        @{ RAM = "Server5"; AvailableRam = 128; UsedRAM = 120 }
    )

    $AvailableRamDataSet = New-UDChartJSDataset -DataProperty AvailableRAM -Label 'Available' -BackgroundColor blue
    $UsedRamDataset = New-UDChartJSDataset -DataProperty UsedRAM -Label 'Used' -BackgroundColor red
    $Options = @{
        Type          = 'bar'
        Data          = $GraphPrep
        Dataset       = @($AvailableRamDataSet, $UsedRamDataset)
        LabelProperty = "RAM"
        Options = @{
            scales = @{
                xAxes = 
                @{
                    stacked = $true
                }            
            yAxes = 
                @{
                    stacked = $true
                }            
            }
        }
    } 

    New-UDChartJS @Options
```

![](<../../../../.gitbook/assets/image (219).png>)

#### Horizontal Bar

![](<../../../../.gitbook/assets/image (146).png>)

```powershell
    $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
    New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName -Options @{
        indexAxis = "y"
        plugins = @{
            legend = @{
                position = "right"
            }
        }
    }p
```

#### Bubble

<figure><img src="../../../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

A bubble chart consists of x and y coordinates and an r value for the radius of the circles.&#x20;

```powershell
$Data = @(
    @{ x = 1; y = 10; r = 15 }
    @{ x = 12; y = 25; r = 35 }
    @{ x = 8; y = 10; r = 95 }
    @{ x = 6; y = 95; r = 25 }
)
New-UDChartJS -Type 'bubble' -Data $Data 
```

#### Line

![](<../../../../.gitbook/assets/image (147).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'line' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Doughnut

![](<../../../../.gitbook/assets/image (148).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'doughnut' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Pie

![](<../../../../.gitbook/assets/image (149).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'pie' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

#### Radar

![](<../../../../.gitbook/assets/image (150).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'radar' -Data $Data -DataProperty CPU -LabelProperty ProcessName
```

### Colors

Colors can be defined using the various color parameters of `New-UDChartJS`.

![](<../../../../.gitbook/assets/image (151).png>)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 

 $Options = @{
   Type = 'bar'
   Data = $Data
   BackgroundColor = 'Red'
   BorderColor = '#c61d4a'
   HoverBackgroundColor = 'Blue'
   HoverBorderColor = '#451dc6'
   DataProperty = 'CPU'
   LabelProperty = 'ProcessName'
 }

 New-UDChartJS @Options
```

### Data Sets

By default, you do not need to define data sets manually. A single data set is created automatically when you use the `-DataProperty` and `-LabelProperty` parameters. If you want to define multiple data sets for a single chart, you can use the `-Dataset` property in conjunction with `New-UDChartJSDataset`.

![](<../../../../.gitbook/assets/image (152).png>)

```powershell
$Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 

 $CPUDataset = New-UDChartJSDataset -DataProperty CPU -Label CPU -BackgroundColor '#126f8c'
 $MemoryDataset = New-UDChartJSDataset -DataProperty HandleCount -Label 'Handle Count' -BackgroundColor '#8da322'

 $Options = @{
   Type = 'bar'
   Data = $Data
   Dataset = @($CPUDataset, $MemoryDataset)
   LabelProperty = "ProcessName"
 }

 New-UDChartJS @Options
```

### Click Events

You can take action when a user clicks the chart. This example shows a toast with the contents of the `$Body` variable. The `$Body` variable contains a JSON string with information about the elements that were clicked.

![](../../../../.gitbook/assets/z4AxJkkVyU.gif)

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 

  $Options = @{
   Type = 'bar'
   Data = $Data
   DataProperty = 'CPU'
   LabelProperty = "ProcessName"
   OnClick = { 
      Show-UDToast -Message $Body
   }
 }


 New-UDChartJS @Options
```

### Auto refreshing charts

You can use `New-UDDynamic` to create charts that refresh on an interval.

![](../../../../.gitbook/assets/CXEz8afan4.gif)

```powershell
New-UDDynamic -Content {
    $Data = 1..10 | % { 
        [PSCustomObject]@{ Name = $_; value = get-random }
    }
    New-UDChartJS -Type 'bar' -Data $Data -DataProperty Value -Id 'test' -LabelProperty Name -BackgroundColor Blue
} -AutoRefresh -AutoRefreshInterval 1
```

### Monitors

Monitors are a special kind of chart that tracks data over time. Monitors are good for displaying data such as server performance stats that change frequently. You return a single value from a monitor and it is graphed automatically over time.

```
New-UDChartJSMonitor -LoadData {
    Get-Random -Max 100 | Out-UDChartJSMonitorData
} -Labels "Random" -ChartBackgroundColor "#297741" -RefreshInterval 1
```

![](../../../../.gitbook/assets/monitor.gif)

### Options

The `New-UDChartJS` cmdlet supports accepting advanced ChartJS options. You can use the `-Options` parameter to pass in a hashtable.&#x20;

This example hides the legend.

```powershell
 $Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
 New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName -Options @{  
 legend = @{  
     display = $false  
 }  
}
```

#### Title

You can include a title with the title option.

```powershell
$Data = Get-Process | Sort-Object -Property CPU -Descending | Select-Object -First 10 
New-UDChartJS -Type 'bar' -Data $Data -DataProperty CPU -LabelProperty ProcessName -Options @{
    plugins = @{
        legend = @{
            title = @{
                display = $true
                text    = 'Bar Chart'
            }
        }
    }
}
```

## Nivo Charts

Universal Dashboard integrates with [Nivo Charts](https://nivo.rocks/components). Below you will find examples and documentation for using these charts.

### Creating a Chart

All the Nivo charts can be created with `New-UDNivoChart`. You will specify a switch parameter for the different types of charts. Each chart type will take a well defined data format via the `-Data` parameter.

![](<../../../../.gitbook/assets/image (86).png>)

```powershell
$Data = 1..10 | ForEach-Object { 
    $item = Get-Random -Max 1000 
    [PSCustomObject]@{
        Name = "Test$item"
        Value = $item
    }
}
New-UDNivoChart -Id 'autoRefreshingNivoBar' -Bar -Keys "value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
```

### Patterns

Nivo provides the ability to specify patterns to display over data sets. You can configure these patterns with `New-UDNivoPattern` and `New-UDNivoFill` .

![](<../../../../.gitbook/assets/image (85).png>)

```powershell
$Data = @(
    @{
        country = 'USA'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Germany'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Japan'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
)

$Pattern = New-UDNivoPattern -Dots -Id 'dots' -Background "inherit" -Color "#38bcb2" -Size 4 -Padding 1 -Stagger
$Fill = New-UDNivoFill -ElementId "fries" -PatternId 'dots'

New-UDNivoChart -Definitions $Pattern -Fill $Fill -Bar -Data $Data -Height 400 -Width 900 -Keys @('burgers', 'fries', 'sandwich')  -IndexBy 'country'
```

### Responsive Widths

Nivo charts provide responsive widths so they will resize automatically when placed on a page or the browser is resized. A height is required when using responsive widths.

![](../../../../.gitbook/assets/responsive.gif)

### Auto Refreshing Charts

Like many components in Universal Dashboard v3, Nivo charts do not define auto-refresh properties themselves. Instead, you can take advantage of `New-UDDynamic` to refresh the chart on an interval.

![](../../../../.gitbook/assets/autorefresh.gif)

```powershell
New-UDDynamic -Content {
    $Data = 1..10 | ForEach-Object { 
        $item = Get-Random -Max 1000 
        [PSCustomObject]@{
            Name = "Test$item"
            Value = $item
        }
    }
    New-UDNivoChart -Id 'autoRefreshingNivoBar' -Bar -Keys "Value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
} -AutoRefresh
```

### OnClick

Nivo charts support OnClick event handlers. You will be provided with information about the data set that was clicked as JSON.

![](../../../../.gitbook/assets/onclick.gif)

```powershell
$Data = @(
    @{
        country = 'USA'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Germany'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
    @{
        country = 'Japan'
        burgers = (Get-Random -Minimum 10 -Maximum 100)
        fries = (Get-Random -Minimum 10 -Maximum 100)
        sandwich = (Get-Random -Minimum 10 -Maximum 100)
    }
)
New-UDNivoChart -Bar -Data $Data -Height 400 -Width 900 -Keys @('burgers', 'fries', 'sandwich')  -IndexBy 'country' -OnClick {
    Show-UDToast -Message $EventData -Position topLeft
}
```

### Types of Charts

#### Bar

```powershell
New-Example -Title 'Bar' -Description '' -Example {
    $Data = 1..10 | ForEach-Object { 
        $item = Get-Random -Max 1000 
        [PSCustomObject]@{
            Name = "Test$item"
            Value = $item
        }
    }
    New-UDNivoChart -Bar -Keys "Value" -IndexBy 'name' -Data $Data -Height 500 -Width 1000
}
```

#### Bubble

![](<../../../../.gitbook/assets/image (97).png>)

```powershell
$TreeData = @{
    Name     = "root"
    children = @(
        @{
            Name  = "first"
            children = @(
                @{
                    Name = "first-first"
                    Count = 7
                }
                @{
                    Name = "first-second"
                    Count = 8
                }
            )
        },
        @{
            Name  = "second"
            Count = 21
        }
    )
}

New-UDNivoChart -Bubble -Data $TreeData -Value "count" -Identity "name" -Height 500 -Width 800
```

#### Calendar

![](<../../../../.gitbook/assets/image (87).png>)

```powershell
$Data = @()
for($i = 365; $i -gt 0; $i--) {
    $Data += @{
        day = (Get-Date).AddDays($i * -1).ToString("yyyy-MM-dd")
        value = Get-Random
    }
}

$From = (Get-Date).AddDays(-365)
$To = Get-Date

New-UDNivoChart -Calendar -Data $Data -From $From -To $To -Height 500 -Width 1000 -MarginTop 50 -MarginRight 130 -MarginBottom 50 -MarginLeft 60
```

#### Heatmap

![](<../../../../.gitbook/assets/image (88).png>)

```powershell
$Data = @(
    @{
        state = "idaho"
        cats = 72307
        dogs = 23429
        moose = 23423
        bears = 784
    }
    @{
        state = "wisconsin"
        cats = 2343342
        dogs = 3453623
        moose = 1
        bears = 23423
    }
    @{
        state = "montana"
        cats = 9234
        dogs = 3973457
        moose = 23472
        bears = 347303
    }
    @{
        state = "colorado"
        cats = 345973789
        dogs = 0237234
        moose = 2302
        bears = 2349772
    }
)
New-UDNivoChart -Heatmap -Data $Data -IndexBy 'state' -keys @('cats', 'dogs', 'moose', 'bears')  -Height 500 -Width 1000 -MarginTop 50 -MarginRight 130 -MarginBottom 50 -MarginLeft 60
```

#### Line

![](<../../../../.gitbook/assets/image (218).png>)

```powershell
[array]$Data = [PSCustomObject]@{
    id = "DataSet"
    data = (1..20 | ForEach-Object {
        $item = Get-Random -Max 500 
        [PSCustomObject]@{
            x = "Test$item"
            y = $item
        }
    })
}
New-UDNivoChart -Line -Data $Data -Height 500 -Width 1000 -LineWidth 1
```

#### Stream

![](<../../../../.gitbook/assets/image (89).png>)

```powershell
$Data = 1..10 | ForEach-Object { 
    @{
        "Adam" = Get-Random 
        "Alon" = Get-Random 
        "Lee" = Get-Random 
        "Frank" = Get-Random 
        "Bill" = Get-Random 
    }
}

New-UDNivoChart -Stream -Data $Data -Height 500 -Width 1000 -Keys @("adam", "alon", "lee", "frank", "bill")
```

#### Treemap

![](<../../../../.gitbook/assets/image (90).png>)

```powershell
$TreeData = @{
    Name     = "root"
    children = @(
        @{
            Name  = "first"
            children = @(
                @{
                    Name = "first-first"
                    Count = 7
                }
                @{
                    Name = "first-second"
                    Count = 8
                }
            )
        },
        @{
            Name  = "second"
            Count = 21
        }
    )
}

New-UDNivoChart -Treemap -Data $TreeData -Value "count" -Identity "name" -Height 500 -Width 800
```
