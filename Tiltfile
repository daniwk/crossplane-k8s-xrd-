docker_build(
    'web-api', # tilt searches for this image name in k8s manifest file below
    context='.',
    dockerfile='./app/Dockerfile',
    only=['./app'],
    # ignore=['./app/sender.py'],
    live_update=[
        sync('./app/', '/app/app/'),
        run(
            'poetry.lock pyproject.toml ./ && pip install --upgrade pip --user',
            trigger=['./pyproject.toml']
        )
    ]
)
k8s_yaml(kustomize('deploy/app'))
k8s_kind('FastAPIInstance', image_json_path='{.spec.parameters.image}')
# k8s_resource(
#     'web-api',
#     labels=['web-api'],
#     objects=['myapp']
# )