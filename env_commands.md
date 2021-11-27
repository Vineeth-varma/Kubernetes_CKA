* Environment Varaibles can be defined in containers section. 
* The fields under "env" can be defined as "Arrays" as shown below
## env types:

### Plain-key Format:
```
env: 
- name: APP_COLOR                    
  value: pink               
```
### ConfigMap Format:
```
env:      # Define the environment variable            
- name: SPECIAL_LEVEL_KEY
  valueFrom:
    configMapKeyRef:           
        name: special-config       # The ConfigMap containing the value you want to assign to SPECIAL_LEVEL_KEY
        key: special.how           # Specify the key associated with the value
```
### Secret Format:
```
env:
- name: SECRET_USERNAME
  valueFrom:
    secretKeyRef:
      name: mysecret
      key: username
- name: SECRET_PASSWORD
  valueFrom:
    secretKeyRef:
      name: mysecret
      key: password
```      
