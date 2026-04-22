function sys = lateral_model(params)

% LATERAL_MODEL  States [v,p,r,phi,psi], input [aileron]

    U0 = params.U0; g = params.g;
    
    A = zeros(5,5);
    
    A(1,1)=params.Yv; A(1,2)=params.Yp; A(1,3)=params.Yr-U0; A(1,4)=g;
    A(2,1)=params.Lv; A(2,2)=params.Lp; A(2,3)=params.Lr;
    A(3,1)=params.Nv; A(3,2)=params.Np; A(3,3)=params.Nr;
    A(4,2)=1; A(5,3)=1;
    
    B = zeros(5,1);
    
    B(1,1)=params.Yda;
    B(2,1)=params.Lda;
    B(3,1)=params.Nda;
    
    sys = ss(A,B,eye(5),0);
    
    sys.StateName = {'v','p','r','phi','psi'};
    
    sys.InputName = {'aileron'};
    
end
