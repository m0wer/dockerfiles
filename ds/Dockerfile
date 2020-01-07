FROM jupyter/scipy-notebook

# Install Python 3 packages
RUN conda install --quiet --yes \
    'geopandas=0.6.*' \
    'folium=0.10.*' \
    'cudf=0.11.*' \
    'ipyleaflet=0.11.*'
 
 
RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'partridge[full]' \
        'modin'
