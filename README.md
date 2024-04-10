# Adjusting-standard-errors-for-spatial-correlation
Spatial correlation allows for correlation between nearby units – for example, correlation between villages located near each other. Instead of clustering at arbitrary administrative variables, such as state boundaries, you can use Conley standard errors to allow for correlation between units within a set distance of each other. The correlation can be constant within that set distance, or decline linearly with distance between units. 

To correct your standard errors for spatial correlation, you can use the command ols_spatial_HAC programmed by Hsiang (PNAS 2010). (This is currently not available through the Stata repository, so you will have to download it at http://www.fight-entropy.com/2010/06/standard-error-adjustment-ols-for.html .). The command also adjusts for heteroskedasticity, and allows for intertemporal correlation if you use panel data. 

The syntax:
ols_spatial_HAC y x, lat(latitude) lon(longitude) distcutoff(cutoff) panelvar(id) timevar(t) lagcutoff(p) barlett

•	longitude and latitude are the coordinates of the observation in degrees;
•	cutoff is the distance in km until which standard errors are allowed to correlate;
•	id is the unique identifier in your data;
•	t is the time variable if you use a panel (if you use a cross-section the syntax requires a constant t to function properly).

There are two further useful options:

•	lagcutoff(p) determines the degree of autocorrelation of errors in panel data (default is p=0); and
•	using barlett specifies that spatial correlation is calculated with a kernel that linearly declines with distance until the cut-off. The default is using a uniform kernel such than the correlation discontinuously jumps to zero at the cut-off. I recommend using the Barlett option.

Lukas Hensel, St Peter's College, Oxford, 18 February 2019
