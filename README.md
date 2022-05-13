# Cold-Tongue-Index

The cold tongue index (CTI) is defined to be average sea surface temperature (SST) anomalies for 6N-6S, 180-90W minus the global-mean SST anomaly (Deser and Wallace, 1990, J. Climate). The global-mean SST is an estimate of the radiative heating of the ocean due to increased greeenhouse gases.  

The CTI captures a lower-frequency signal of the El Niño / Southern Oscillation phenomenon than the Nino3.4 index, which is decribed at https://github.com/ToddMitchellGH/ENSO-nino3.4-timeseries/blob/master/README.md.  That README.md also documents the temperature and precipitation anomalies associated with fluctuations in the CTI/Nino3.4.

I am calculating the CTI from the Extended Reconstructed Sea Surface Temperature (ERSST; Huang et al., 2017, J. Climate) dataset, which is served by NOAA ESRL
wget https://downloads.psl.noaa.gov/Datasets/noaa.ersst.v5/sst.mnmean.nc .

NetCDF commands are used to calculate the global-mean SST and CTI: 
ncwa -O -h -a lat,lon -d lat,-6.0,6.0 -d lon,180.0,270.0 sst.mnmean.nc a.nc

ncap2 -h -O -s "weights=cos(lat*3.1415/180)" sst.mnmean.nc sst.mnmean.nc
ncwa -h -O -w weights -a lat,lon sst.mnmean.nc sstglobalmean1854jan2022.nc

ncdiff a.nc sstglobalmean1854jan2022.nc cti1854jan2022.nc

Plots of the CTI and global-mean SST are presented at https://sites.google.com/site/toddmitchellgeophysics
