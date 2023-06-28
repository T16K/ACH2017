# Problemas de Instalação

Este relatório aborda os problemas encontrados durante a execução e construção do projeto WotPy, disponível no [GitHub](https://github.com/agmangas/wot-py). 

## Fork e Clone do Projeto

Inicialmente, foi realizado um fork do projeto WotPy e o [repositório](https://github.com/T16K/wot-py) foi clonado para o computador. 

## Construção do Projeto com Docker

Ao tentar construir o projeto utilizando o `docker build .`, deparou-se com um erro relacionado à versão do pacote numpy. A mensagem de erro foi a seguinte:
```
ERROR: Could not find a version that satisfies the requirement numpy==1.22.0 (from versions: 1.3.0, 1.4.1, 1.5.0, 1.5.1, 1.6.0, 1.6.1, 1.6.2, 1.7.0, 1.7.1, 1.7.2, 1.8.0, 1.8.1, 1.8.2, 1.9.0, 1.9.1, 1.9.2, 1.9.3, 1.10.0.post2, 1.10.1, 1.10.2, 1.10.4, 1.11.0, 1.11.1, 1.11.2, 1.11.3, 1.12.0, 1.12.1, 1.13.0, 1.13.1, 1.13.3, 1.14.0, 1.14.1, 1.14.2, 1.14.3, 1.14.4, 1.14.5, 1.14.6, 1.15.0, 1.15.1, 1.15.2, 1.15.3, 1.15.4, 1.16.0, 1.16.1, 1.16.2, 1.16.3, 1.16.4, 1.16.5, 1.16.6, 1.17.0, 1.17.1, 1.17.2, 1.17.3, 1.17.4, 1.17.5, 1.18.0, 1.18.1, 1.18.2, 1.18.3, 1.18.4, 1.18.5, 1.19.0, 1.19.1, 1.19.2, 1.19.3, 1.19.4, 1.19.5, 1.20.0, 1.20.1, 1.20.2, 1.20.3, 1.21.0, 1.21.1, 1.21.2, 1.21.3, 1.21.4, 1.21.5, 1.21.6)
ERROR: No matching distribution found for numpy==1.22.0
The command '/bin/sh -c pip install -r requirements.txt' returned a non-zero code: 1
```

Para solucionar esse problema, foi tentada inicialmente a alteração da versão do Python no arquivo Dockerfile (https://github.com/T16K/wot-py/commit/b8e9d090e738b343a825cd404f63dde950954a70).

Posteriormente, optou-se por utilizar a versão original do Python (3.7) e, no arquivo "examples/benchmark/requirements.txt", foi revertida a versão modificada pelo dependabot[bot] (https://github.com/agmangas/wot-py/commit/61bec7348c6342c05fd8d2c3ccb21dad60aed58b).

Por fim, a solução adotada foi remover a inclusão das dependências do diretório /examples/benchmark no Dockerfile, mantendo a modificação anterior (https://github.com/agmangas/wot-py/commit/3dd4f7e428bd565970adf96f8f4482cf986496ea). Essa decisão foi tomada considerando que o exemplo do benchmark não seria utilizado no projeto, e, portanto, as dependências relacionadas a ele não seriam necessárias.

## Execução dos Testes

A execução dos testes do WoTPy foi iniciada com o seguinte comando:
```
./pytest-docker-all.sh
```

Após a construção, foi identificado o seguinte erro:
```
Traceback (most recent call last):
        File "<string>", line 2, in <module>
        File "<pip-setuptools-caller>", line 34, in <module>
        File "/app/setup.py", line 58, in <module>
          setup(
        File "/usr/local/lib/python3.10/site-packages/setuptools/__init__.py", line 87, in setup
          return distutils.core.setup(**attrs)
        File "/usr/local/lib/python3.10/site-packages/setuptools/_distutils/core.py", line 185, in setup
          return run_commands(dist)
        File "/usr/local/lib/python3.10/site-packages/setuptools/_distutils/core.py", line 201, in run_commands
          dist.run_commands()
        File "/usr/local/lib/python3.10/site-packages/setuptools/_distutils/dist.py", line 968, in run_commands
          self.run_command(cmd)
        File "/usr/local/lib/python3.10/site-packages/setuptools/dist.py", line 1217, in run_command
          super().run_command(command)
        File "/usr/local/lib/python3.10/site-packages/setuptools/_distutils/dist.py", line 987, in run_command
          cmd_obj.run()
        File "/usr/local/lib/python3.10/site-packages/wheel/bdist_wheel.py", line 395, in run
          self.egg2dist(self.egginfo_dir, distinfo_dir)
        File "/usr/local/lib/python3.10/site-packages/wheel/bdist_wheel.py", line 534, in egg2dist
          pkg_info = pkginfo_to_metadata(egginfo_path, pkginfo_path)
        File "/usr/local/lib/python3.10/site-packages/wheel/metadata.py", line 160, in pkginfo_to_metadata
          for key, value in generate_requirements({extra: reqs}):
        File "/usr/local/lib/python3.10/site-packages/wheel/metadata.py", line 138, in generate_requirements
          for new_req in convert_requirements(depends):
        File "/usr/local/lib/python3.10/site-packages/wheel/metadata.py", line 103, in convert_requirements
          parsed_requirement = Requirement(req)
        File "/usr/local/lib/python3.10/site-packages/wheel/vendored/packaging/requirements.py", line 37, in __init__
          raise InvalidRequirement(str(e)) from e
      wheel.vendored.packaging.requirements.InvalidRequirement: Expected end or semicolon (after version specifier)
          coverage>=5.0<6.0
                  ~~~~~^
      [end of output]
```

Para lidar com esse problema, o arquivo setup.py foi editado (https://github.com/T16K/wot-py/commit/b8e9d090e738b343a825cd404f63dde950954a70):

## Resultados

Dessa forma, o WoTPy pôde ser construído corretamente utilizando o Docker e passou nos testes propostos no "pytest-docker-all.sh".
