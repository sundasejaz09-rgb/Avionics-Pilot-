function sys = longitudinal_model(params)
% LONGITUDINAL_MODEL  States [u,w,q,theta], input [elevator]
    U0 = params.U0; g = params.g;
    A = zeros(4,4);
    A(1,1)=params.Xu; A(1,2)=params.Xw; A(1,3)=0; A(1,4)=-g;
    A(2,1)=params.Zu; A(2,2)=params.Zw; A(2,3)=U0+params.Zq; A(2,4)=0;
    A(3,1)=params.Mu+params.Mwd*params.Zu;
    A(3,2)=params.Mw+params.Mwd*params.Zw;
    A(3,3)=params.Mq+params.Mwd*(U0+params.Zq); A(3,4)=0;
    A(4,:)=[0,0,1,0];
    B = zeros(4,1);
    B(1,1)=params.Xde;
    B(2,1)=params.Zde;
    B(3,1)=params.Mde+params.Mwd*params.Zde;
    sys = ss(A,B,eye(4),0);
    sys.StateName = {'u','w','q','theta'};
    sys.InputName = {'elevator'};
end
