
# Open for All

News • Careers • Life in Tech
Skills • Resources

FOSSlife.org

### Listing 3: solar_2.pl

```perl
#!/usr/bin/perl

# Usage: ./solar_2.pl forecast.csv profile.csv power

use DateTime;

my $csv_forecast;
my $csv_profile;

my $line_number = 0;
open (my $forecast, '<', $ARGV[0]) or die "Failed to open $ARGV[0]";
while ( my $line = <$forecast> ) {
    $line =~ s/\r//;
    chomp ($line);

    my ($power,$timestamp) = (split ",", $line)[0,1];
    ${csv_forecast[$line_number]}["power"] = $power;
    ${csv_forecast[$line_number]}["timestamp"] = $timestamp;

    ++$line_number;
}
close ($forecast);

$line_number = 0;
open (my $profile, '<', $ARGV[1]) or die "Failed to open $ARGV[1]";
while ( my $line = <$profile> ) {
    chomp ($line);

    my ($timestamp, $percentage) = (split ",", $line);
    ${csv_profile[$line_number]}["timestamp"] = $timestamp;
    ${csv_profile[$line_number]}["percentage"] = $percentage;

    ++$line_number;
}
close ($profile);

# For each 30 minutes period, calculate whether we are
# going to produce
# more power than we are going to consume (and therefore waste it),
# or whether we are going to consume more power than we produce (and
# therefore have deficit).

my $waste = 0;
my $deficit = 0;
my $produced = 0;

my ( $y,$m,$d,$h,$mt,$sec );
my ( $i,$j );
for ( $i = 1 ; $i < @csv_forecast ; ++$i ) {
    ( $y,$m,$d ) = ${csv_forecast[$i]}["timestamp"] =~ m/^(\d+)\/(\d+)\/(\d+)$/;
    ($h,$mt,$sec) = ${csv_forecast[$i]}["timestamp"] =~ /\/(\d+)\/(\d+)\/(\d+)\/(\d+)\/(\d+)\/(\d+)Z/;

    unless ( defined ($h) && ($h,$mt,$sec) eq ('0', '0', '0') ) {
        my $forecast_time = DateTime->new(
            year => $y,
            month => $m,
            day => $d,
            hour => $h,
            minute => $mt,
            second => $sec,
            time_zone => 'UTC'
        );

        $forecast_time->set_time_zone('local');

        my $consumption;

        my ($hour,$minute );
        for ( $j = 1 ; $j < @csv_profile ; ++$j ) {
            ($hour,$minute) = ${csv_profile[$j]}["timestamp"] =~ m/(\d+):(\d+)/;

            if ( $hour eq $forecast_time->hour() and $minute eq $forecast_time->minute() ) {
                $consumption = ${csv_profile[$j]}["percentage"] * $ARGV[2] * 0.01;
            }
        }

        if ( $consumption > (${csv_forecast[$i]}["power"] * 0.5) ) {
            $deficit += ${consumption} - (${csv_forecast[$i]}["power"] * 0.5 );
        } else {
            $waste += (${csv_forecast[$i]}["power"] * 0.5 ) - ${consumption};
        }

        ${produced} += ${csv_forecast[$i]}["power"] * 0.5;

        # If the day has changed, print information for the
        # day.
        if ( $forecast_time->hour() eq "0" and $forecast_time->minute() eq "0") {
            ${forecast_time->subtract({ days => 1})};
            print "INFORMATION FOR DATE " . ${forecast_time->date()} . "\n";
        }
    }
    $deficit = 0;
    $waste = 0;
    $produced = 0;
}
exit;
```

timestamp of the entry of the forecast file. Lines 55-64 create a `DateTime` object corresponding to the timestamp and adjust it to the local time zone.

Lines 68-75 look in the profile file for the entry corresponding to the timestamp it is currently analyzing and calculate the total power you expect the house to consume in that period. This calculation multiplies the total energy use expected for the day by the percentage of daily power use expected in the period corresponding to the timestamp, divided by 100. The result, in kilowatt-hours, is stored in the `$consumption` variable.

The calculations in lines 76-80 are the energy debt and excess. If the house consumes more power than is produced, the script notes the energy debt in the `$deficit` variable. Otherwise, excess power is noted in the `$waste` variable.

The script also records the power produced so far by the solar array during the day in line 82.

Line 85 guesses whether the end of the day has arrived. If so, the script prints the information corresponding to the day just parsed and sets `$deficit`, `$waste`, and `$produced` to zero to start the next day anew.

## Conclusion

The script in Listing 3 is a proof of concept and lacks input validation. It does not check whether the CSV files fed to it are correct and lacks appropriate exit statuses for input errors. However, it serves as a base on which to build a prediction system. You can easily set up a cronjob to download a forecast file from Solcast each day at midnight, generate a prediction with the script, and send it by email or post it to a website. The possibilities are endless (Figure 8).

A more complex script that supports input validation and tracks the state of the battery banks is available at my gophersite [6]. (You’ll need a gopher client.)

**Info**

- [1] Solcast irradiance prediction service: https://solcast.com.au/
- [2] IDAE residential consumption in Spain: https://www.idaes.es/uploads/documents/documents_Documentacion_Basica_Residencial_Unido_c30da537.pdf (in Spanish)
- [3] US EIA energy use in homes: https://www.eia.gov/energyexplained/use-of-energy/electricity-use-in-homes.php
- [4] UK household energy usage: https://www.ukpower.co.uk/home-energy/average-household-gas-and-electricity-usage
- [5] Power output of the Spanish power grid, February 2022: https://demanda.ree.es/visions/pensula/demandaqh/tablas/2022-11-2/1 (in Spanish)
- [6] Rubén Lorente’s gophersite: gopher://gopher.operationalsecurity.es/1/Software

```bash
devuan@developer:~$ perl solar_2.pl forecast.csv profile2.csv 9.55
INFORMATION FOR DATE 2022-11-05
Total power produced will be 13.22555 kWh
About 5.71888868822784 kWh will be taken from the grid (deficit)
About 9.42324045014541 kWh will be produced but not used (wasted)

INFORMATION FOR DATE 2022-11-07
Total power produced will be 9.47265 kWh
About 5.903870468880704 kWh will be taken from the grid (deficit)
About 5.8561222308062 kWh will be produced but not used (wasted)

INFORMATION FOR DATE 2022-11-08
Total power produced will be 7.8111 kWh
About 6.10894940562567 kWh will be taken from the grid (deficit)
About 3.59965116754404 kWh will be produced but not used (wasted)
devuan@developer:~$
```

![](img/e3f454b04d121b3b3750fddfda8dd21e_68_0.png)

## Author

Rubén Lorente is a mechanical engineer who ensures that the IT security measures for a small clinic are both legally compliant and safe. In addition, he is an OpenBSD enthusiast and a weapons collector.

![](img/e3f454b04d121b3b3750fddfda8dd21e_68_1.png)

![](img/e3f454b04d121b3b3750fddfda8dd21e_68_2.png)
