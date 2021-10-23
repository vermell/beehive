# This target allows us to bundle our app into a PEX binary file via
#  `./pants package`. We can also run it with `./pants run`. See
#  https://www.pantsbuild.org/docs/python-package-goal and
#  https://www.pantsbuild.org/docs/python-run-goal.

pex_binary(
    name = "pex_binary",
    entry_point = "src/beehive/elasticfluent/__main__.py",
)

python_tests(
    name = "test_elasticfluent",
    sources = ["test/**/*.py"],
)

docker_image(
    name="helloworld",
    dependencies=[":pex_binary"],
)