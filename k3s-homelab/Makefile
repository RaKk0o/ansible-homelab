VENV_PATH := venv

PLAYBOOK_NAME := cluster.yml

ANSIBLE_BIN := $(VENV_PATH)/bin/ansible-playbook
ANSIBLE_OPTIONS := -i inventory.yml --become --diff

all:
	@echo "type 'make cluster' to deploy the cluser"

$(VENV_PATH)/bin/pip:
	virtualenv $(VENV_PATH)

$(VENV_PATH)/bin/ansible-playbook: $(VENV_PATH)/bin/pip
	"$<" install ansible==9.2.0
	$(VENV_PATH)/bin/ansible-galaxy install -r requirements.yml

ansible-config:
	export ANSIBLE_ENABLE_TASK_DEBUGGER=True

cluster: $(VENV_PATH)/bin/ansible-playbook ansible-config
	"$<" $(ANSIBLE_OPTIONS) $(PLAYBOOK_NAME)

clean:
	rm -rfI $(VENV_PATH)

.PHONY: all ansible-config cluster clean

