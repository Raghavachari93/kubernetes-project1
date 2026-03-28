<h1>Kubernetes Project 1 — Deploy Nginx on Minikube</h1>

<p>
This project demonstrates a <strong>real-world Kubernetes deployment</strong> using <strong>Minikube</strong>. 
You will deploy an <strong>Nginx web application</strong>, expose it using a <strong>NodePort Service</strong>, 
and understand how Kubernetes manages containerized applications.
</p>

<hr>

<h2>Project Goal</h2>

<p>
Simulate a <strong>real DevOps workflow</strong>:
</p>

<ul>
  <li>Developers build an application → containerize it</li>
  <li>DevOps engineers deploy it → Kubernetes cluster</li>
  <li>Users access the application → via Service</li>
</ul>

<p>
This project is ideal for beginners learning:
<strong>Kubernetes, DevOps, container orchestration, and deployment strategies</strong>.
</p>

<hr>

<h2>Architecture Overview</h2>

<pre>
User → Service → Pod → Container (Nginx)
</pre>

<ul>
  <li><strong>Pod</strong>: Runs the container</li>
  <li><strong>Deployment</strong>: Manages pods and ensures availability</li>
  <li><strong>Service</strong>: Exposes the application to users</li>
</ul>

<hr>

<h2>📁 Project Structure</h2>

<pre>
kubernetes-project1/
│
├── deployment.yaml
├── service.yaml
└── README.md
</pre>

<hr>

<h2>⚙️ Step 1 — Start Minikube</h2>

<pre><code>minikube start</code></pre>

<p>Verify cluster:</p>

<pre><code>kubectl get nodes</code></pre>

<hr>

<h2>📄 Step 2 — Create Deployment</h2>

<p><strong>deployment.yaml</strong></p>

<pre><code>
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
</code></pre>

<h3>🔍 Key Concepts</h3>

<ul>
  <li><strong>replicas: 2</strong> → Ensures high availability</li>
  <li><strong>selector</strong> → Links Deployment to Pods</li>
  <li><strong>template</strong> → Blueprint for Pods</li>
  <li><strong>image</strong> → Docker image (Nginx)</li>
</ul>

<p>Apply deployment:</p>

<pre><code>kubectl apply -f deployment.yaml</code></pre>

<p>Verify:</p>

<pre><code>
kubectl get deployments
kubectl get pods
</code></pre>

<hr>

<h2>📄 Step 3 — Create Service</h2>

<p><strong>service.yaml</strong></p>

<pre><code>
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
      nodePort: 30007
</code></pre>

<h3>🔍 Key Concepts</h3>

<ul>
  <li><strong>NodePort</strong> → Exposes app outside cluster</li>
  <li><strong>selector</strong> → Connects service to pods</li>
  <li><strong>port</strong> → Service port</li>
  <li><strong>nodePort</strong> → External access port (30000–32767)</li>
</ul>

<p>Apply service:</p>

<pre><code>kubectl apply -f service.yaml</code></pre>

<p>Verify:</p>

<pre><code>kubectl get services</code></pre>

<hr>

<h2>🌐 Access the Application</h2>

<pre><code>minikube service nginx-service</code></pre>

<p>
This will automatically open your browser and display the <strong>Nginx Welcome Page</strong>.
</p>

<hr>

<h2>🧪 Verification Checklist</h2>

<ul>
  <li>✅ Nginx welcome page loads</li>
  <li>✅ 2 pods are running</li>
  <li>✅ Service is exposing the application</li>
</ul>

<hr>

<h2>🧨 Hands-On Learning (Break & Learn)</h2>

<h3>1️⃣ Delete a Pod</h3>

<pre><code>kubectl delete pod &lt;pod-name&gt;</code></pre>

<p>Kubernetes will automatically recreate it.</p>

<h3>2️⃣ Scale Deployment</h3>

<pre><code>kubectl scale deployment nginx-deployment --replicas=4</code></pre>

<h3>3️⃣ Check Logs</h3>

<pre><code>kubectl logs &lt;pod-name&gt;</code></pre>

<hr>

<h2>Common Mistakes</h2>

<ul>
  <li>Incorrect labels (Service won’t connect)</li>
  <li>Port mismatches</li>
  <li>Forgetting to start Minikube</li>
  <li>Using invalid NodePort range</li>
</ul>

<hr>

<h2>Optional Enhancements</h2>

<ul>
  <li>Increase replicas (3–5)</li>
  <li>Customize Nginx HTML page</li>
  <li>Use <code>kubectl describe</code> for debugging</li>
</ul>

<hr>

<h2>Interview Insight</h2>

<p><strong>Q: What happens when a pod crashes?</strong></p>

<blockquote>
Deployment ensures the desired state. If a pod fails, Kubernetes automatically recreates it.
</blockquote>

<hr>

<h2> Learning Outcomes</h2>

<ul>
  <li>Kubernetes Deployment</li>
  <li>Service (NodePort)</li>
  <li>Pod lifecycle management</li>
  <li>Scaling and self-healing</li>
</ul>

<hr>



<p>
Kubernetes project, Minikube tutorial, Kubernetes deployment example, Nginx Kubernetes, 
DevOps beginner project, Kubernetes NodePort service, container orchestration, 
Kubernetes hands-on project, Kubernetes GitHub project.
</p>

<hr>



<p>
If you found this helpful, consider giving this repository a ⭐ and sharing it with others learning Kubernetes!
</p>
