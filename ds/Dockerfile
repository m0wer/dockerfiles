FROM jupyter/minimal-notebook

USER root

# ffmpeg for matplotlib anim
RUN apt-get update && \
    apt-get install -y --no-install-recommends ffmpeg \
                                               graphviz \
                                               openjdk-8-jdk && \
    rm -rf /var/lib/apt/lists/*

USER $NB_UID

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'ipywidgets' \
        'jupyter_contrib_nbextensions' \
        'matplotlib' \
        'widgetsnbextension'

# Activate ipywidgets extension in the environment that runs the notebook server
RUN jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # Also activate ipywidgets extension for JupyterLab
    # Check this URL for most recent compatibilities
    # https://github.com/jupyter-widgets/ipywidgets/tree/master/packages/jupyterlab-manager
    jupyter labextension install @jupyter-widgets/jupyterlab-manager@3.0.0 --no-build && \
    jupyter labextension install @bokeh/jupyter_bokeh@2.0.4 --no-build && \
    # jupyter labextension install jupyter-matplotlib --no-build && \
    jupyter lab build --dev-build=False && \
    jupyter contrib nbextension install --sys-prefix && \
    #jupyter labextension install jupyterlab-dash && \
    npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER

# Import matplotlib the first time to build the font cache.
ENV XDG_CACHE_HOME /home/$NB_USER/.cache/
RUN MPLBACKEND=Agg python -c "import matplotlib.pyplot" && \
    fix-permissions /home/$NB_USER

RUN pip install --upgrade pip && \
    pip install --no-cache-dir \
        'scikit-learn'

RUN pip install --no-cache-dir \
        'autopep8' \
        'bokeh' \
        'git+git://github.com/cgupm/crtm_poll' \
        'dask' \
        'folium' \
        'gdown' \
        'geopandas' \
        'graphviz' \
        'ipyleaflet' \
        'jupyterlab-dash' \
        'kaleido' \
        'mlinsights' \
        'modin[ray]' \
        'mrjob' \
        'pandarallel' \
        'partridge[full]' \
        'plotly' \
        'psutil' \
        'psycopg2-binary' \
        'pyquickhelper' \
        'pyspark' \
        'sqlalchemy' \
        'statsmodels' \
        'sympy' \
        'xgboost'
