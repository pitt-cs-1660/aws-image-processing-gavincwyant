FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# copy requirements file
COPY pyproject.toml ${LAMBDA_TASK_ROOT}/

# copy handler
COPY handler.py ${LAMBDA_TASK_ROOT}/

# install dependencies using uv
RUN uv venv ${LAMBDA_TASK_ROOT}/.venv && \
    uv pip install --python ${LAMBDA_TASK_ROOT}/.venv/bin/python -r pyproject.toml

# set PYTHONPATH to include the virtual environment site-packages
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages:${LAMBDA_TASK_ROOT}"

# set the CMD to your handler
CMD [ "handler.exif_handler" ]
