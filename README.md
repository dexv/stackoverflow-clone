<h1 align="center">Implementando Docker + Kubernetes en GCP. Un ejemplo práctico: Clon de Stackoverflow construido con React/Next y Node</h1>

<div align="center">Proyecto original de <a href="https://github.com/salihozdemir/stackoverflow-clone" target="_blank">salihozdemir/stackoverflow-clone</a></div>

<h3 align="center">
  <a href="http://clone-of-stackoverflow.vercel.app/">Visitar la aplicación en vivo</a>
</h3>

## Crear el namespace y definir namespace creado por defecto

```
cd stackoverflow-clone
kubectl apply -f namespace.yaml
kubectl config set-context --current --namespace=stackoverflow
```

# BackEnd

## Crear secret

Reemplazar los valores de las llaves `PORT` y `DATABASE_URL`. Para usar este comando en Linux/MacOS se debe reemplazar `^` por `\`

```
kubectl create secret generic stackoverflow-credentials ^
    --from-literal=PORT=8060 ^
    --from-literal=DATABASE_URL=mongodb://mongoadmin:secret@192.168.1.84/stackoverflow ^
    -n stackoverflow
```

## Crear imagen

```
cd stackoverflow-clone\server
docker build -t stackoverflow-backend-img .
```

## Ejecutar el deployment

```
cd stackoverflow-clone\server
kubectl apply -f deployment.yaml
```

# FrontEnd

## Crear imagen

```
cd stackoverflow-clone\client
docker build -t stackoverflow-frontend-img .
```

## Ejecutar el deployment

```
cd stackoverflow-clone\client
kubectl apply -f deployment.yaml
```

## URL 

```
http://localhost:8061/
```

## :memo: License

This project is made available under the MIT License.
